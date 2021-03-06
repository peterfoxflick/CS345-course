![](../images/banner.jpg)

# Ponder 08 : OpenMP Lab

##### Due Monday night at Midnight MST

This week, you will be implementing a program that with producer and consumer threads.

You will be to modify our threads matrix multiplication program so it uses OpenMP.

The first step in the coding projects is to write the code.

### A. Start with Lab 05

Start with your (hopefully) working matrix multiplication code from Lab 05\. There will be some sample code provided:

<pre>/home/cs345/week08/</pre>

Here you will find several files:

*   `makefile` : A makefile to build lab08.cpp and the sample programs
*   `lab08.cpp` : Same code we started Lab 05 with
*   `sampleVariableThreads.cpp` : Create multiple threads using OpenMP

Make sure you update the header in the makefile so it gets submitted to the correct location. The assignment this week will be called `Lab 08, OpenMP`

You will also need to write a prompt to ask the user for the number of threads to use:

<pre>% lab08.out 2x3.txt 2x2.txt
How many threads? 5
| -1 -4  |   |  2  3  |   | -22 -15   |
|  4  1  | X |  5  3  | = |  13  15   |
|  6  2  |                |  22  24   |</pre>

### B. Write the code

Add the OpenMP code to enable threads and parallel processing.

#### Include the OpenMP compiler directives

OpenMP works through compiler directives. The programmer includes a collection of `#pragma` statements informing the OpenMP library how many threads are to be created, which variables are shared, and which are private.

#### Hints

A few issues that you may run into:

*   **-fopenmp** : Compile your code with `-fopenmp`.

    <pre>g++ sampleVariableThreads.cpp -fopenmp</pre>

*   **_OPENMP** : You can determine if OpenMP is configured on your system:

    <pre>#ifdef _OPENMP
       cout << "_OPENMP defined, threadct = " << threadct << endl;
    #else
       cout << "_OPENMP not defined" << endl;
    #endif</pre>

*   **pragma**: To request a parallel computation, add the following pragma preprocessor directive, just before the for loop. The “`\`” is a line continuation character and must not be followed by any character, not even white space.

    <pre>#pragma omp parallel num_threads(2) \
                shared(x)</pre>

*   **omp parallel for** : The strings `omp parallel for` indicate that this is an OpenMP pragma for parallelizing the for loop that follows immediately. The OpenMP system will divide the various iterations of that loop up into `threadct` segments, each of which can be executed in parallel on multiple cores.

    <pre>#pragma omp parallel for num_threads(10)</pre>

*   **private** : The clauses in the second line indicate whether the variables that appear in the for loop should be shared with the other threads, or should be local private variables used only by a single thread. Here, three of those variables are globally shared by all the threads (`a, b, c`), and only one (`x`) is local to each particular thread:

    <pre>#pragma omp parallel for num_threads(numThreads) \
              shared (a, b, c) private(x) </pre>

There are several tutorials on OpenMP that you may want to consult.

[Lawrence Livermore National Laboratory : OpenMP](https://computing.llnl.gov/tutorials/openMP/)

[OpenMP.org : OpenMP Application Program Interface](http://openmp.org/mp-documents/OpenMP4.0.0.Examples.pdf)

### C. Verify

The testBed for this assignment is:

<pre>testBed cs345/lab08 lab08.tar</pre>

Please make sure your program runs without error.

#### Style

Your program should be well-commented and free of any style errors.

## Submit

Please submit your TAR file that is created by the makefile.

### Grading

Your submission will be graded according to the following criteria:

<table class="rubric">

<tbody>

<tr>

<th> </th>

<th>Exceptional  
100%</th>

<th>Good  
90%</th>

<th>Acceptable  
70%</th>

<th>Developing  
50%</th>

<th>Missing  
0%</th>

</tr>

<tr>

<th>Correct  
20%</th>

<td>No defects could be found</td>

<td>The code works as designed, including passing testBed</td>

<td>One test failed to pass on testBed or one glaring bug exists in the code</td>

<td>Elements of the solution exist</td>

<td>No attempt was made to solve the problem</td>

</tr>

<tr>

<th>Efficient  
50%</th>

<td>It is difficult to imagine how the code could be made more efficient</td>

<td>No obvious efficiency problems exist</td>

<td>One minor thing could be done to improve the efficiency of the code</td>

<td>Many obvious opportunities exist to increase performance</td>

<td>The code has horrible performance issues</td>

</tr>

<tr>

<th>Elegant  
10%</th>

<td>The most elegant solution imaginable was found</td>

<td>The code looks "professional"</td>

<td>One minor inelegancy was found</td>

<td>One obvious inelegancy remains in the code</td>

<td>The code was thrown together</td>

</tr>

<tr>

<th>Maintainable  
10%</th>

<td>The code lends itself to reuse and extension</td>

<td>The solution is well designed and thought out</td>

<td>One aspect of the solution design could be improved</td>

<td>Obvious maintainability problems exist</td>

<td>Support costs on this code would be much greater than necessary</td>

</tr>

<tr>

<th>Readable  
10%</th>

<td>"Anyone" could read and understand this code</td>

<td>The code honors all the style guidelines</td>

<td>One minor style error was found</td>

<td>One obvious style error was found</td>

<td>No obvious attention was spent on readability</td>

</tr>

</tbody>

</table>
