# Dynamic Programming for Hessian Chain Bracketing

## To build

make

Note: Eigen is expected to be installed in / linked to the ./Eigen subdirectory

## To run

./generate.exe N M 
  ... generates a problem with N as the compositeness and 
  M as the upper bound on the dimensions of the Jacobians. 

./solve.exe problem.txt
  ... solves for optimizing the cost of accumulation of Hessian 
  along with the sample results of bracketing from left and right
  for comparison purposes. Creates a bracketing order and saves it
  in "solution.txt" to be given as input for run.exe. It also creates
  a heuristic bracketing order and saves it in "heuristic_solution.txt"
  and this too is given as an input to the run.exe
  
./run.exe problem.txt solution.txt heuristic_solution.txt
  ... takes the input file "problem.txt" from generate.exe and input file
  "solution.txt" and "heuristic_solution.txt" from solve.exe and compares 
  the run times of the bracketing approaches from right and left and the 
  naive heuristic bracketing against the Dynamic programming algorithm for 
  calculating the Hessian by performing actual Tensor and matrix multiplications.
  

## Example

a)	./generate.exe 4 4 > problem.txt

Yields the following input file(please note that the dimensions generated here are 
subject to change during subsequent running of the software owing to the random
ness in the problem generation). The input file generated below has the following 
data:
	1) The compositeness of the function, represented as "4" below.
	2) The dimensions of the individual Jacobians are shown in the 
	first chunk of values. 
		eg. 5, 2 are the dimensions in x and y direction for the 
		first Jacobian and so on.

4
5 2
1 5
3 1
2 3

b)	./solve.exe problem.txt

yields following output:

left bracketing fma = 342
right bracketing fma = 230
heuristic bracketing fma = 156
optimized bracketing fma = 156

Dynamic Programming Table:
fma(F''(1,0))=90; Split before 1; dim(F''(1,0))=1x2x2
fma(F''(2,1))=165; Split before 2; dim(F''(2,1))=3x5x5
fma(F''(2,0))=130; Split before 2; dim(F''(2,0))=3x2x2
fma(F''(3,2))=30; Split before 3; dim(F''(3,2))=2x1x1
fma(F''(3,1))=146; Split before 2; dim(F''(3,1))=2x5x5
fma(F''(3,0))=156; Split before 2; dim(F''(3,0))=2x2x2



c)	./run.exe problem.txt solution.txt heuristic_solution.txt

we provide 3 input files for this part. The first is the result generated 
from generate.exe, the second and third are the results generated from solve.exe.
The output generated from solve.exe which is stored in "solution.txt"
is the optimized bracketing order for the hessian chaining problem obtained
by running the Dynamic programming in solve.exe. Similarly the ouput stored 
in "heuristic_solution.txt" is the bracketing order concerning the naive heuristic
bracketing algorithm. 

Running the above command yields the elapsed time (subject to slight changes) 
for left bracketing, right bracketing, heuristic bracketing and the optimized 
bracketing approach.

Elapsed time (in microseconds):
left bracketing: 36
right bracketing: 22
heuristic bracketing: 6
optimized bracketing: 14

NOTE :: The results presented in the paper can be easily reproduced  
by the input files present in the folder "Tested_input_files". 
