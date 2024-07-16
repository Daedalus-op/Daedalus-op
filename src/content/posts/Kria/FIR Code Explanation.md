# Table of Content
- [Python](#python)
- [HLS Code](#hls-code)
	- [Base Code](#base-hls-code-for-fir-filter)
	- [Loop Pipelining](#loop-pipelining)
	- [Code Hoisting](#code-hoisting)
	- [Code Unrolling](#code-unrolling)
	- [Unrolling vs Pipelining](#unrolling-vs-pipelining)
# Python 
In the cookbook the scipy function `scipy.signal.lfilter()` is used for filtering a singal. A pure and non optimized python (with NumPy) implementation would look like:
```python
def fir (x, h):
	nsamples = len(x)
	N = len(h)
	y = np.zeros(len(x))
	shift_reg = np.zeros(len(N))
	
	for j in range(nsamples):
		acc = 0
		for i in range(N-1, 0, -1):
			shift_reg[i] = shift_reg[i - 1]
			acc += shift_reg[i] * h[i]
		acc += x[j] * h[0]
	
		shift_reg[0] = x[j]
		y[j] = acc
	return y
```
# HLS Code
### Base HLS code for FIR filter
Notice there is no compiler directives for optimization for HLS flow :-
```cpp
#define N 11
#include "ap_int.h"

void fir(int *y, int x){
	int c[N] = {1,2,3,4,5,6,7,8,9,10,11};
	static 
	int shift_reg[N];
	int acc;
	int i;

	acc = 0;
	shift_acc_loop:
	for (i = N - 1; i >= 0; i--){
		if(i == 0){
			shift_reg[0] = x;
			acc = c[0] * x;
		} else {
			shift_reg[i] = shift_reg[ i - 1 ];
			acc += c[i] * shift_reg[i];
		}
	}
	*y = acc;
}
```
### Loop Pipelining
In the previous code we execute each loop serially one after the other. Loop pipelining exists to parallelize this. Starting the next iteration before the previous one ends. 
Insert this line after loop definition of the loop you are optimizing.
```cpp
#pragma HLS pipeline II=N
```
`#pragma` is a compiler directive to tweak the RTL flow 
So ...
```cpp
	acc = 0;
	shift_acc_loop:
	for (i = N - 1; i >= 0; i--){
	#pragma HLS pipeline II = 1 // Sets Initial inveterval to 1. Lesser II, More parallelism 
		if(i == 0){
			shift_reg[0] = x;
```
### Code Hoisting
The above code doesn't work completely because of over generalization of initial iteration. This can be solved by bringing the initial iteration outside. This is code hoisting.
```cpp
	for (i = N - 1; i > 0; i--){
		shift_reg[i] = shift_reg[ i - 1 ];
		acc += c[i] * shift_reg[i];
	}
	shift_reg[0] = x;
	acc = c[0] * x;
	*y = acc;
```
Alternately we can use ternary operators instead
```cpp
for (int i = N - 1; i >= 0; i--){
	shift_reg[i] = (i==0) ? x[s] : shift_reg[i - 1];
	int x_temp = (i==0) ? x[s] : shift_reg[i];
	acc += x_temp * c[i];
}
```
### Code Unrolling
Also used to increase parallelism by replicating the loop body parallelly. Done by adding the following line after loop.
```cpp
#pragma HLS unroll
```
The code becomes
```cpp
for (int i = N - 1; i >= 0; i--){
#pragma HLS unroll
	shift_reg[i] = (i==0) ? x[s] : shift_reg[i - 1];
	int x_temp = (i==0) ? x[s] : shift_reg[i];
	acc += x_temp * c[i];
}
```
In the above code, the all the registers need to be accessed in parallel. Therefore we need to make them individual registers instead of part of memory stack To allow this be make one more addition to the code.

```cpp
	#pragma HLS ARRAY_PARTITION variable=shift_reg
```
This maps the c array to N registers. 
```cpp
	int c[N] = {1,2,3,4,5,6,7,8,9,10,11};
	static 
	int shift_reg[N];
	#pragma HLS ARRAY_PARTITION variable=shift_reg
	int acc;
	int i;

	acc = 0;
	shift_acc_loop:
	for (i = N - 1; i >= 0; i--){
```

### Unrolling vs Pipelining

| Unrolling               | Pipelining                   |
| ----------------------- | ---------------------------- |
| Same type of operations | Different type of Operations |
| Different Data          | Same Data                    |

**Similarities**
Increases Parallelism 
Can be used together 