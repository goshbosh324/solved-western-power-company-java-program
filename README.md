Download Link: https://assignmentchef.com/product/solved-western-power-company-java-program
<br>
<ol>

 <li>Introduction</li>

</ol>

The Western Power Company (WPC) has an electrical grid that allows it to deliver electricity to its customers. The grid consists of a set of electrical switches and cables. A new customer C wants to know whether WPC can provide electricity to its property. For this assignment, you will design and implement a program in Java to determine whether the electrical grid of WPC can deliver power to the new customer

C: The program needs to determine whether the set of electrical switches of WPC’s grid can be used to form a path from WPC (where the electricity is generated) to C ‘s house.

You are given a map of the city, which is divided into rectangular cells to simplify the task of computing the required path. There are different types of map cells:

<ul>

 <li>an initial map cell, where WPC is located,</li>

 <li>a map cell where the house of customer C is situated,</li>

 <li>map cells containing blocks of houses of other customers,</li>

 <li>map cells containing electrical switches. There are 3 types of electrical switches:</li>

 <li>omni switches. An omni switch located in a cell L can be used to interconnect all the neighboring map cells Of L. A cell L has at most 4 neighboring cells that we will denote as the north, south, east, and west neighbors. The omni switch can be used to interconnect all neighbors of L;</li>

 <li>vertical switches. A vertical switch can be used to connect the north and south neighbors of a map cell;</li>

 <li>horizontal switches, A horizontal switch can be used to connect the east and west neighbors of a map cell.</li>

</ul>

The following figure shows an example of a map divided into cells. Each map cell has up to 4 neighboring cells indexed from O to 3. Given a cell, the north neighboring cell has index O and the remaining neighboring cells are indexed in clockwise order. For example, in the figure the neighboring cells of cell 6 are indexed from O to 3 as follows: Neighbor with index O is cell 3, neighbor with index I is cell 5, neighbor with index 2 is cell 7, and neighbor with index 3 is cell 11. Note that some cells have fewer than 4 neighbors and the indices of these neighbors might not be consecutive numbers; for example, cell 9 in the figure has 3 neighbors indexed O, l, and 3.

A path from the WPC cell (cell number 1 in the figure) to C’s house (cell number 10) is the following: l, 2, 3, 4, 5, 6, 7, 9, 10. Note that a path cannot go from cell 3 to cell 6, because the horizontal switch in cell 3 only connects cells 2 and 4. Similarly from cell 5 a path cannot go to cell 8; also from cell 8 it is not possible to go to cell 10. Since cell 11 does not contain a switch, such a cell cannot be pan of a path from WPC to C.

<strong>1.1 Valid Paths </strong>

When looking for a path the program must satisfy the following conditions:

<ul>

 <li>The path can go from the WPC cell or from an omni switch cell to the following neighboring cells:</li>

 <li>the customer cell</li>

 <li>an omni switch cell</li>

 <li>the north cell or the south cell, if such a cell is a vertical switch</li>

 <li>the east cell or the west cell, if such a cell is a horizontal switch.</li>

 <li>The path can go from a vertical switch cell to the following neighboring cells:</li>

 <li>The north cell or the south cell, if such a cell is either the customer cell C, an omni switch cell or a vertical switch cell</li>

 <li>The path can go from a horizontal switch cell to the following neighboring cells:</li>

 <li>The east cell or the west cell, if such a cell is either the customer cell C, am omni switch cell, or a horizontal switch cell.</li>

</ul>

If while looking for a path the program finds that from the current cell there are several choices as to which adjacent cell to use to continue the path, your program must select the next cell for the path in the following manner.

<ul>

 <li>the program prefers the customer cell over the other cells;</li>

 <li>if there is no customer cell adjacent to the current cell, then the program must prefer the omni switch cell over the other cells;</li>

 <li>if there is no omni switch cell the program chooses the smallest indexed cell that satisfies the conditions described above.</li>

</ul>

<ol start="2">

 <li><strong> Classes to Implement </strong></li>

</ol>

A description of the classes that you need to implement in this assignment is given below. You can implement more classes, if you want. You cannot use any static instance variables. You cannot use java’s provided Stack class or any of the other java classes from the java library that implements collections. The data structure that you must use for this assignment is an array, as described in Section 2.1.

<strong>2.1 ArrayStack.java </strong>

This class implements a stack using an array. The header of this class must be this:

public class <em>ArrayStack&lt;T&gt;</em> implements <em>ArrayStackADT&lt;T&gt;</em>

You can download ArrayStackADT.java from the course’s website. This class will have the following

private instance variables:

<ul>

 <li><em>private T [] stack</em>. This array will store the data items of the stack.</li>

 <li><em>private int top.</em> This variable stores the position of the last of data item in the stack. In the constructor this variable must be initialized to -l, this means that the stack is empty. Note that this is different from the way in which the variable lop is used in the lecture notes.</li>

</ul>

This class needs to provide the following public methods.

<ul>

 <li><em>public ArrayStack().</em>Creates an empty stack. The default initial capacity of the array used to store the items of the stack is 20.</li>

 <li><em>public ArrayStack (int initial capacity).</em> Creates an empty stack using an array Of length equal to the value of the parameter</li>

 <li><em>public void push (T dataitem)</em> Adds dataitem to the top of the stack. If the array storing the data items is full, you will increase its capacity as follows:</li>

 <li>If the capacity of the array is smaller than 100, then the capacity of the array Will be increased by a factor of 2.</li>

 <li>Otherwise, the capacity of the array will increase by 50. So, if, for example, the size of</li>

 <li>the array is 100 and the array is full, when a new item is added the size of the array Will increase to 150</li>

 <li><em>public T pop () throws</em> Removes and returns the data item at the top of the stack. An <em>EmptyStackException</em> is thrown if the stack is empty. If after removing a data item from the stack the number of data items remaining is smaller than one third of the length of the array you need to shrink the size of the array by half; to do this create a new array of size equal to half of the size of the original array and copy the data items there.</li>

</ul>

For example, if the stack is stored in an array of size 100 and it contains 34 data items, after performing a pop operation the stack will contain only 33 data items. Since 33 &lt; 100/3 then the size of the array will be reduced to 50.

When creating an <em>EmptyStackException</em> appropriate String message must be passed as parameter.

<ul>

 <li><em>public T peek () throws EmptyStackException.</em> Returns the data item at the top of the stack without removing it. An <em>EmptyStackException</em> thrown if the stack is empty.</li>

 <li><em>public boolean isEmpty</em> (). Returns true if the stack is empty and it returns false otherwise.</li>

 <li><em>public int size ().</em> Returns the number of data items in the stack.</li>

 <li><em>public int length ().</em> Returns the length or capacity of the stack array.</li>

 <li><em>public String to String ().</em> Returns a String representation of the stack of the form:</li>

</ul>




“Stack: elem1, elem2, …” where elem1 is a String representation of the

<em>i-th</em> stack. If, for example, the stack is stored in an array called s, then elem1 is s[0].<em> toString ()</em> elem2 is s [1]. <em>toString</em>() and so.

You can implement other methods in this class, if you want to, but they must be declared as private.

<strong>2.2 FindConnection.java </strong>

This class will have an instance variable

<em>Map citymap;</em>

This variable Will reference the Object representing the city map where WPC and C are located. This

variable must be initialized in the constructor for the class, as described below. You must implement the

following methods in this class:

<ul>

 <li><em>public FindConnection</em> <em>(String filename).</em> This is the constructor for the class. It receives as input the name of the file containing the description of the city map. In this method you must create an object of the class Map (described in Section 5) passing as parameter the given input file; this will display the map on the screen. Some sample input files are also provided in the course’s website. Read them if you want to know the format of the input files.</li>

 <li>public static void main (string [] args). This method will first create an Object Of the class FindConnection using the constructor FindConnection(args[0]) When you run the program, you will pass as command line argument the name of the input file (see Section 4). Your main method then Will try to find a path from the WPC cell to the destination cell C according to the restrictions specified above. The algorithm that looks for a path from the initial cell to the destination must use a stack and it cannot be recursive. Suggestions on how to look for this path are given in the next section. The code provided to you Will show the path selected by the algorithm as it tries to reach the customer cell C, so you can visually verify if your program works. private cell) The parameter is the current cell. This method returns the best cell to continue the path from the current one, as specified in Section 1.1. If several unmarked cells (details about marked and unmarked cells are given in Sections 3 and 5) are adjacent to the current one and can be selected as part of the path (as described in Section 1.1), then this method must return one of them in the following Order:</li>

 <li>the customer cell</li>

 <li>an omni switch cell (if the conditions Of Section 1.1 are satisfied). If there are several possible omni switch cells satisfying the conditions of Section 1.1, then the one with smallest index is returned. Read the description of the class below to learn how to get the index of a neighboring cell</li>

 <li>a vertical or horizontal switch cell with smallest index that satisfies the conditions stated in Section 1.1</li>

</ul>

If there are no unmarked cells adjacent to the current one that can be used to continue the path,

this method returns null.

Your program must catch any exceptions that might be thrown. For each exception caught an appropriate message must be printed. The message must explain what caused the exception to be thrown.

You can write more methods in this class, if you want to, but they must be declared as private.

<ol start="3">

 <li><strong> Algorithm for Computing a Path </strong></li>

</ol>

Below is a description of an algorithm for looking for a path from the WPC cell to the destination cell C.

Make sure you understand the algorithm before you implement it. You do not need to implement this

algorithm. You are encouraged to design your own algorithm, but it must use a stack to keep track of

which cells have been processed and it cannot be recursive. You are encouraged to first write a detailed

algorithm in pseudocode before implementing it in Java.

<ul>

 <li>Create an empty stack.</li>

 <li>Get the starting WPC cell using the methods of the supplied class Map (description of this class is given below).</li>

 <li>Push the starting cell into the stack and mark the cell as inStack. You will use methods of the class <em>MapCell</em> to mark a cell.</li>

 <li>While the stack is not empty and the destination has not been found perform the following steps:</li>

 <li>Peek at the top of the stack to get the current cell.</li>

 <li>If the current cell is the destination, then the algorithm exits the loop.</li>

 <li>Otherwise, find the best unmarked neighboring cell (use method from class to do this). If this cell exists, push it into the stack and then mark it as otherwise, since there are no unmarked neighboring cells that can be added to the path pop the top cell from the stack and mark it as<em> outOfStack</em></li>

</ul>

Your program must print a message indicating whether the destination was reached or not. If a path was found the algorithm must also print the number of cells in the path from the initial cell to the destination.

Notice that your algorithm does not need to find the shortest path from the starting cell to the destination.

<ol start="4">

 <li><strong> Command Line Arguments </strong></li>

</ol>

Your program must read the name of the input map file from the command line. You can run the program with the following command:

java

where is the name of the file containing the city map You can use the following

code to verify that the program was invoked with the correct number of arguments:

Sta tie void

must provide the name of the input file”);

string =;

To get Eclipse to supply a command line argument to your program open the “Run -&gt;Run

Configurations…” menu item. Make it Sure that the “Java is the active selection on the left-hand side. Select the “Arguments” tab. Enter the name of the file for the map in the “Program arguments” text box.

<img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2019/02/702.png?w=980&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2019/02/702.png?w=980&amp;ssl=1" data-recalc-dims="1">

 </noscript>