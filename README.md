Download Link: https://assignmentchef.com/product/solved-cs1010-assignment-5
<br>
Question 1: Contact——————————

Contact tracing is an important step to contain theon-going pandemic.  Suppose we are given the informationon who is in contact with who.  We wish to answer thefollowing question:

– Given two people A and B, have they been directly incontact with each other?

– Given two people A and B, is there a common person thatthey have been in contact with?  In other words, is therea third person C, where (i) A and C have been in contactwith each other, and (ii) B and C have been in contactwith each other?

We assume that “contact” is a symmetric relation.  If A hasbeen in contact with B, then B has been in contact withA too.  Because of this, we can represent the contacttraces between n people as a lower triangular matrix(_using jagged 2D array_).  A proper type to store ineach element of the matrix is `bool`.  To simplify ourlife, however, we store each element of the matrix as a`char`, with `’1’` representing a friendship connection,`’0’` otherwise. The contact traces for n people is thus anarray of n strings, each string containing characters of`’0’` and `’1’` only.  The first row of the matrix is astring of length one; the second row is of length two;third row, length three, etc.  The last character ofeach string (i.e., the diagonal of the matrix) is `1`since everyone has contact with him/herself.

For instance, suppose we have the following contact traces.We represent each person with id 0, 1, 2, …  Person withid i has its information stored in Row i and Column i.Recall that if Row i and Column j is 1, it means thatPerson i has been in contact with Person j.“`101011“`

The contact traces above indicates that Person 1 and 2have been in contact with each other.  Person 0 has notbeen in contact with either.

As another example, the contact traces below shows anextra person, Person 4.“`1010111011“`

Person 4 has been in contact with both Person 1 andPerson 3.

Write a program `contact`, that reads from standard input:

– a positive integer n,– followed by n lines of strings consisting of `’1’` or`’0’` representing the social network of these n people.– followed by two positive integers m and n, representingthe ids of a pair of people we are interested in querying.An input of i corresponds to the person whose contactinformation is stored in Row i and Column i.

Print, to the standard output, the following information:

– `direct contact` if there is direct contact between mand n– `contact through x` if there is no direct contact butthere is an indirect contact between m and n through athird person x (replace x with the actual id).  If thereare multiple such third person, output the one with thesmallest id.– `no contact` if there is no direct nor indirect contactthrough a third person in the contact traces.

The purpose of this question is for you to practiceusing a jagged 2D array.  Hence, _you are not allowed tostore the input matrix or intermediate matrices using arectangular array_, or you risk being penalized heavilyfor this question.

### Sample Run“`<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="aec1c1c7d9daeedecb9f9f97">[email protected]</a>:~/as05-skeleton$ cat inputs/contact.1.in31110110 1<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="117e7e786665516174202028">[email protected]</a>:~/as05-skeleton$ ./social &lt; inputs/contact.1.indirect contact<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="4e212127393a0e3e2b7f7f77">[email protected]</a>:~/as05-skeleton$ cat inputs/contact.2.in31110110 2<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="036c6c6a747743736632323a">[email protected]</a>:~/as05-skeleton$ ./social &lt; inputs/contact.2.incontact through 1<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="3a5555534d4e7a4a5f0b0b03">[email protected]</a>:~/as05-skeleton$ cat inputs/contact.3.in410101110110 1<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="345b5b5d434074445105050d">[email protected]</a>:~/as05-skeleton$ ./contact &lt; inputs/contact.3.inno contact“`

Question 2: Social ——————————

You should solve this question after solving Question 1.The functions you wrote for Question 1 might be usefulfor solving this question.

The idea of six degrees of separation states that everyonein the world is connected to every other person by at most6 hops. Suppose that a person A is a friend of a personB, then we say that A is one hop away from B. Consider afriend of B, say C, who is not a friend of A. So C is afriend of a friend of A. We say that C is two hops awayfrom A.  Six degrees of separation generally means thereis a chain of friendship that can connect any two peoplein the world with no more than 6 hops.

In this question, we are going to compute the chain offriendships up to the k degree. Suppose there are n people,and we know the social network of these n people — i.e.,we know who is a friend with who. Write a program `social`to compute a social network representing who is connectedto who via a friendship chain of degree k.

Similar to Question 1, we assume that friendship isbi-directional — if A is a friend of B, then B is afriend of A.  We represent a social network as a lowertriangular matrix (using jagged 2D array) in the sameformat as Question 1, where a `1` in Row i and Column jmeans Person i and Person j are friends; `0` otherwise.

The social network below shows the friendship relationsbetween four people.

“`1010111011“`

Suppose now we consider the social network of degree2. Person 0 is two hops away from Person 2 (Person 0 knowsPerson 3, and Person 3 knows Person 2). Person 1 is alsotwo hops away from Person 3 (Person 1 knows Person 2 andPerson 2 knows Person 3).

The social network of degree 2 becomes:“`1011111111“`

Write a program `social`, that reads from standard inputtwo positive integers n and k, followed by n linesof strings consisting of ‘1’ or ‘0’ representing thesocial network of these n people.  Print, to the standardoutput, the social network formed by a friendship chainof degree k.

The purpose of this question is for you to practiceusing a jagged 2D array. Hence, you are not allowed tostore the input matrix or intermediate matrices using arectangular array, or you risk being penalized heavilyfor this question.

### HintThere are many ways to solve this problem.  The moststraightforward way is to compute the social network formedby a friendship chain of degree i, N(i), changing i from1 to k.

– N(1) is just the input;– N(2) can be computed similar to how you solved Question 1.– Now, given N(i-1) and N(1), can you compute N(i)?

### Sample Run————–“`<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="442b2b2d333004342175757d">[email protected]</a>:~/as05-skeleton$ cat inputs/social.1.in3 1111011<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="96f9f9ffe1e2d6e6f3a7a7af">[email protected]</a>:~/as05-skeleton$ ./social &lt; inputs/social.1.in111011<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="f19e9e988685b18194c0c0c8">[email protected]</a>:~/as05-skeleton$ cat inputs/social.2.in4 21010111011<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="9ef1f1f7e9eadeeefbafafa7">[email protected]</a>:~/as05-skeleton$ ./social &lt; inputs/social.2.in1011111111<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="680707011f1c28180d595951">[email protected]</a>:~/as05-skeleton$ cat inputs/social.3.in5 2111011001110011<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="98f7f7f1efecd8e8fda9a9a1">[email protected]</a>:~/as05-skeleton$ ./social &lt; inputs/social.3.in111111111111111“`

## Question 3: Life——————————

This question is another tribute to John H. Conway,who passed away in April this year due to COVID-19.The Game-of-Life is among his famous mathematical endeavors(in addition to the Look-n-Say sequence).

The “Game of Life” is a game played on a two-dimensionalorthogonal grid of square cells, while each cell hasonly two possible states: alive or dead. The game isplayed in iterations. During each iteration, each cellbecomes alive or dead, depending on the state of its fourneighboring cells in the previous iteration. Interestingpatterns and moving behavior can be created, sometimesinfinitely, from an initial state. Refer to [wikipage](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life)for more details if you are interested.

In this problem, we are going to simulate a game of lifefor a certain number of iterations, given a startingstate. Here is a complete description of the rules ofthe simulation.

1. The universe is a bounded plane and can be simplyreferred to as a two-dimensional orthogonal grid of squarecells with n rows and m columns. For convenience, we letrow indexes as 0 to n-1 from top to bottom, and columnindexes as 0 to m-1 from left to right. So in total,there are n X m cells.

2. The neighbor of a cell is defined as the eight cellsthat are either horizontally, vertically, or diagonallyconnected to the cell.

3. An initial state is given, with each cell is marked aseither “live” or “dead”.

4. In each iteration, a cell may switch its state,according to rules below, by referring to the state ofthe previous iteration:

* Any live cell with fewer than two live neighbors becomes dead* Any live cell with two or three live neighbors remains alive.* Any live cell with more than three live neighbors becomes dead.* Any dead cell with exactly three live neighbors becomes alive* Border cells, i.e., cells with row number 0 or $n-1$, or columnnumber 0 or $m-1$, are always dead. This is to simplify andbound the universe.

Write a program `life` that reads, from the standardinputs, three positive integers n (n &gt; 2), m (m &gt; 2) andk, where n and m denote the number of rows and number ofcolumns of the universe (an n x m grid), and k is thenumber of iterations to simulate.  It then reads, fromthe standard input, n rows, with m characters in each rowrepresenting the initial state.  Each character is eitheralive (`#`) or dead (`.`).

The program then prints, to standard output, an animationof the universe for k iterations.  The output should onlycontain n rows with m characters in each row.  Similarly,you must use `#` to represent a live cell, and `.` torepresents a dead cell.

### Animation on Screen

We have provided a few lines of code in the skeleton file.You should insert this at appropriate places:

“`cs1010_clear_screen();// TODO(by student) draw the universeusleep(250*1000);“`

Line 1 in the code above calls a function from the CS1010I/O library which clears your screen and places the cursoron the top left corner of the terminal.   Line 3 callsthe system function `usleep` that takes in the numberof microseconds.  Calling `usleep` causes the programto pause for that amount of time.  We set the sleepingtime to 250ms.  You can reduce if you wish but you mustnot increase this beyond 250ms or your program might failwhen we test it during grading.

### Sample Run

– The pattern from `life.1.in` is called a blinker.– The pattern from `life.2.in` is called a pentadecathlon.– The pattern from `life.4.in` is called a pulsar.

We provide a total of seven patterns for you to play with.You can run“`~cs1010/life &lt; inputs/life.1.in“`for instance, to observe the output from the program.

### Testing and Debugging

Note that `make` will not automatically test `life`for you.  Before you submit, you should check your outputis correct, by running“`./test.sh life“`manually.  If you do so, you may wish to reduce thesleeping time or do not call `usleep` altogether to speedup testing.  Sleeping time only affects the animation,not the correctness of the output.

To help you debug, you can redirect the output from lifeinto a file, and use `vim -d` to view the differences.“`<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="e08f8f899794a09085d1d1d9">[email protected]</a>:~/as05-skeleton$ ./life &lt; inputs/life.3.in &gt; OUT<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="c1aeaea8b6b581b1a4f0f0f8">[email protected]</a>:~/as05-skeleton$ vim -d OUT outputs/life.3.out“`