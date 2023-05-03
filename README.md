Download Link: https://assignmentchef.com/product/solved-cs310-project-2-tent-tree-game-3
<br>
<strong><u>Topics Covered</u></strong>

Linked Lists, Hashing

Overview

You are going to build a simplified version of <strong>Tree-Tent</strong> puzzle using Hashing. The main idea is to place tents on a 2D grid with initial placement of trees to meet all these conditions:

<ol>

 <li>Every tree must be connected to a tent;</li>

 <li>Every tent must be attached to a tree;</li>

 <li>No two tents are adjacent to each other, neither horizontally, vertically, or diagonally.</li>

</ol>

For two things to be connected or attached, they must be adjacent either horizontally or vertically.  For example, given (A) as an initial puzzle, (B) is a valid solution while (C) is not since one tree is missing a tent and also two tents are touching each other.







(A)                                            (B)                                      (C)

(Picture src: http://www.chiark.greenend.org.uk/~sgtatham/puzzles/js/tents.html)




There are many similar websites providing helpful description and online playing.  For example: <u>http://www.brainbashers.com/tentshelp.asp</u> has a good explanation of rules.  Notice we are implementing a simplified version for this project.  You do NOT need to support the additional restriction of how many tents are allowed to be placed on each row/column.







<h1>Implementation</h1>

<table width="228">

 <tbody>

  <tr>

   <td width="64">(0,0)</td>

   <td width="60">(0,1)</td>

   <td width="28">…</td>

   <td width="76">(0,M-1)</td>

  </tr>

  <tr>

   <td width="64">(1,0)</td>

   <td width="60">…</td>

   <td width="28">…</td>

   <td width="76">(1,M-1)</td>

  </tr>

  <tr>

   <td width="64">…</td>

   <td width="60">…</td>

   <td width="28">…</td>

   <td width="76">…</td>

  </tr>

  <tr>

   <td width="64">(N-1,0)</td>

   <td width="60">(N-1,1)</td>

   <td width="28">…</td>

   <td width="76">(N-1,M-1)</td>

  </tr>

 </tbody>

</table>

We are using a hash map to implement the 2D grid for our game.  The map stores &lt;cell, symbol&gt; pairs for all non-empty cells of our puzzle.   Suppose every cell on the board with N rows and M columns is represented with a (row_index, column_index) as shown to the right.  For every cell at (r,c) that is occupied by a symbol S, we will have a pair &lt;(r, c), S&gt; in our hash map.  For example, the board represented in Figure (A)

above should include three entries as {(&lt;0,0&gt;,Tree), (&lt;2,3&gt;,Tree),(&lt;3,1&gt;, Tree)} (not necessarily in that order).  All puzzle moves (adding a tent, removing a tent, checking a tent, etc) are therefore performed via hash map operations.




We are following the idea described in Ch6.8 of our textbook to implement the hash map using a set with a &lt;key, value&gt; pair.  What is special is that equals/hashCode implementations of the &lt;key, value&gt; pair is based on the key only.  The class implementing the hash map (HashMap.java) is implemented and provided to you.  But you will need to implement the underlying set which keeps a unordered collection of no duplicates and supports fast retrival/searach/removal.  This must be implemented as a hash table with separate chaining to resolve collision in HashTable.java.  You must also implement your own linked list to use in the hash table as SimpleList.java.




<h1>Classes Overview <u> </u></h1>




There are a total of <strong>6</strong> classes in the project but two of them are fully implemented and provided to you. Make sure you check the project package for required methods and additional details.




<strong>Position (Position.java)</strong>: This class represents the cell position in a 2-D grid. In addition to the normal accessors, you also need to implement .equals and .hashCode to compare two positions and to return an integer hash code.  Remember to follow hash contract and pick a hash function that is easy to compute and distribute well.

<strong> </strong>

<strong>SimpleList(SimpleList.java)</strong>: This class is a generic linked list that you will use to implement separate chaining in hash table. You can choose how the linked list is organized as far as the required operations are supported with the specified runtime overhead.  You also need to define a basic iterator for this class and implement efficient .hasNext() and .next() in it.




<strong>HashTable(HashTable.java)</strong>: This class is a generic hash table using separate chaining to resolve collision. The table is initialized as an array of 11 spots but may need to be expanded.  In addition to the load, we will also be monitoring the average chain length of all active buckets.  You are required to expand and rehash to a bigger hash table if the average chain length is &gt; 1.2.  The new table size must be a prime number larger than twice the size before.  A .nextPrime() is provided for you to use. <em>Definition</em>: <strong>Average chain length</strong> = number of elements / non-empty active chains.




<strong>HashMap(HashMap.java)</strong>: This class is a generic hash map (dictionary) implemented using

HahTable.java.  <u>This class is fully written and provided to you</u>, including a Pair class that makes sure both .equal and .hashCode are determined only by the key of a &lt;key, value&gt; pair.  Read the code to understand how HashTable class will be used.




<strong>TentTree</strong>: This class is the primary class representing the tent-tree puzzle. It consists of the tenttree board stored as an instance of HashMap class. The class contains methods to add and remove tents, to check whether at least one of the 4-way or 8-way neighbors of the specified position has the given symbol, to check if the puzzle has solved or not. Make sure to utilize the fast retrieval/search of the hash map to implement the operations when possible. A .toString() is provided to you to help testing and debugging.  The puzzle status checking is considered as <strong><u>extra credit</u></strong> (5%).




<strong>PA2</strong>: This class provides a basic user interface for you to play the game interactively once your implementation is in place.  <u>This class is fully written and provided to you</u>. It accepts a .txt file to initialize the board.  The user can then add/remove tents to find a solution of the puzzle.  Even if you do not implement the extra credit part for status checking, you can still play (and maybe manually verify whether you are done).  A set of puzzle files are provided to you for testing purpose.




<strong> </strong>







<h1>Big-O</h1>




Template given to you in the starter package contains instructions on the REQUIRED Big-O runtime for each method. Your methods should not have a higher Big-O and you will be graded on this.







<h1>Testing</h1>




Test cases will not be provided for this project. However, feel free to create test cases by yourselves. In addition, the main methods provided along with the template classes contain useful code to test your code. You can use command like “java Position” to run the testing defined in main( ).  You could also edit main( ) to perform additional testing.  And yes, a part of your grade will be based on automatic grading using test cases that are not provided to you.







<strong>EXAMPLE RUN #1 </strong>

<strong> java</strong> <strong>PA2 puzzles/puzzle1.txt</strong>

–     –     –

O     –     O

–     –     O







Please select what you’d like to do:

<ul>

 <li>Exit</li>

 <li>Add a tent</li>

 <li>Remove a tent</li>

 <li>Check whether the puzzle has been solved</li>

</ul>

2




Please select where you’d like to add the tent (X): which row (0-2):

0 which col (0-2):

0

X     –     –

O     –     O

–     –     O







Please select what you’d like to do:

<ul>

 <li>Exit</li>

 <li>Add a tent</li>

 <li>Remove a tent</li>

 <li>Check whether the puzzle has been solved 4</li>

</ul>

unfinished puzzle: tree missing tent!

X     –     –

O     –     O

–     –     O







Please select what you’d like to do:

<ul>

 <li>Exit</li>

 <li>Add a tent</li>

 <li>Remove a tent</li>

 <li>Check whether the puzzle has been solved</li>

</ul>

2




Please select where you’d like to add the tent (X):

which row (0-2):

0 which col (0-2):

2

X     –     X

O     –     O

–     –     O







Please select what you’d like to do:

<ul>

 <li>Exit</li>

 <li>Add a tent</li>

 <li>Remove a tent</li>

 <li>Check whether the puzzle has been solved</li>

</ul>

2




Please select where you’d like to add the tent (X): which row (0-2):

2 which col (0-2):

0

X     –     X

O     –     O

X     –     O







Please select what you’d like to do:

<ul>

 <li>Exit</li>

 <li>Add a tent</li>

 <li>Remove a tent</li>

 <li>Check whether the puzzle has been solved</li>

</ul>

3




Please select where you’d like to remove a tent (X): which row (0-2):

2 which col (0-2):

0

X     –     X

O     –     O

–     –     O







Please select what you’d like to do:

<ul>

 <li>Exit</li>

 <li>Add a tent</li>

 <li>Remove a tent</li>

 <li>Check whether the puzzle has been solved</li>

</ul>

2




Please select where you’d like to add the tent (X):

which row (0-2):

2 which col (0-2):

1

X     –     X

O     –     O

–     X     O







Please select what you’d like to do:

<ul>

 <li>Exit</li>

 <li>Add a tent</li>

 <li>Remove a tent</li>

 <li>Check whether the puzzle has been solved</li>

</ul>

4

Puzzle solved!

Congratulations!!!













<h1><u>EXAMPLE RUN #2 </u></h1>

<strong> </strong>

<strong>java</strong> <strong>PA2 puzzles/puzzle1.txt</strong>

–     –     –

O     –     O

–     –     O







Please select what you’d like to do:

<ul>

 <li>Exit</li>

 <li>Add a tent</li>

 <li>Remove a tent</li>

 <li>Check whether the puzzle has been solved</li>

</ul>

3




Please select where you’d like to remove a tent (X): which row (0-2):

0 which col (0-2):

0

Cannot remove tent(X) at row 0 col 0!

<ul>

 <li>–    –</li>

</ul>

O     –     O

<ul>

 <li>– O</li>

</ul>







Please select what you’d like to do:

<ul>

 <li>Exit</li>

 <li>Add a tent</li>

 <li>Remove a tent</li>

 <li>Check whether the puzzle has been solved</li>

</ul>

2




Please select where you’d like to add the tent (X): which row (0-2):

1 which col (0-2):

0

Cannot add a tent (X) at row 1 col 0!

<ul>

 <li>– –</li>

</ul>

O     –     O

<ul>

 <li>– O</li>

</ul>







Please select what you’d like to do: 1) Exit

<ul>

 <li>Add a tent</li>

 <li>Remove a tent</li>

 <li>Check whether the puzzle has been solved</li>

</ul>


