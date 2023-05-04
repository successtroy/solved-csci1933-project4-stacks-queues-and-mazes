Download Link: https://assignmentchef.com/product/solved-csci1933-project4-stacks-queues-and-mazes
<br>
In this project, you will use Stacks and Queues to solve basic mazes. A maze is a network of paths designed so there is at least one path from the entrance of the maze to the exit of the maze. You will be using a queue structure to find this correct path through the maze, and a stack structure to randomly generate new mazes.

1.1       Files Given

Along with the project write-up, you will be given the following files:

<ul>

 <li><strong>java </strong>The main java class for this project</li>

 <li><strong>java </strong>A helper class for MyMaze</li>

 <li><strong>java </strong>– Both the queue and stack structure will utilize this generic node class</li>

 <li><strong>java </strong>– An interface for a generic queue</li>

 <li><strong>java </strong>– An implementation of a generic queue</li>

 <li><strong>java </strong>– An interface for a generic stack</li>

 <li><strong>java </strong>– An implementation of a basic stack</li>

</ul>

You will not change any of the files given except for the class called MyMaze. All other files are provided with everything you should need.

1.2         Stack and Queue data structures

Both the stack and queue data structures provided have basic functionality. Take a look at both classes to ensure you know how to instantiate and use them properly. They should be similar to the examples you have seen in lecture.

<ol start="2">

 <li>CELL</li>

</ol>

<h1>2           Cell</h1>

You do not need to change the Cell class, but this section describes how a cell works. The Cell class has the following attributes:

boolean visited – true if this cell has been visited, false otherwise boolean right – true if a right boundary, false if an open right side boolean down – true if a lower boundary, false if an open bottom

Each of these attributes have setter and getter functions respectively. The Cell constructor initializes the cell to have walls on the right and bottom. When we say a cell has been visited, assume we are referring to the visited attribute unless otherwise noted. The purpose for each attribute will become evident in the MyMaze section below.

<h1>3           MyMaze</h1>

The MyMaze class is where the majority of the work will take place. There will be three main functions for the maze class:

public static MyMaze makeMaze(int rows, int cols); public void printMaze(boolean path); public void solveMaze();

More detail about each function will be found in their respective sections. The MyMaze class will have one main attribute: Cell[][] maze. The maze attribute will be how the maze is represented.

This attribute will have the following properties:

<ul>

 <li>The start of the maze will always be the upper left: maze[0][0] (open on the left)</li>

 <li>The end of the maze will always be in the lower right: maze[rows-1][cols-1] (open on the right)</li>

 <li>All Cells on the ”top” (row 0) have an implicit top boundary</li>

 <li>All cells of the ”left” (column 0) have an implicit left boundary</li>

 <li>Once initialized, the maze should have a path from the beginning to the end of the maze.</li>

</ul>

For example, a maze of size 5×20 that could be generated is shown in Figure 1.

3.1       Constructor

The MyMaze constructor should have the following signature: public MyMaze(int rows, int cols); It should just instantiate the maze attribute: maze = new Cell[rows][cols] and create a new cell object for each index: maze[i][j] = new Cell().

<ol start="3">

 <li>MYMAZE</li>

</ol>

Figure 1: 5×20 Maze; Path = False

3.2      makeMaze

This function should instantiate a new MyMaze object, generate the maze, and then return the new MyMaze object. This will build a maze from scratch by utilizing a stack. By choosing randomly which direction to go from a particular cell, and visiting every cell, there should be a path from the entrance to every cell, including the exit. You can do this by implementing the following search algorithm:

<ul>

 <li>Initialize a stack with the start index {0, 0}. Mark this cell (maze[0][0]) as visited.</li>

 <li>Loop until the stack is empty:

  <ul>

   <li>Get the top element off the stack but do not remove it.</li>

   <li>Choose a random neighbor to the corresponding cell that has not been visited and do the following:</li>

  </ul></li>

</ul>

∗ Add the neighbor’s index to the stack.

∗ Mark the neighbor as visited.

∗ Remove the wall between the current cell and the neighbor cell.

<ul>

 <li>If the current cell does not have any un-visited neighbors, then it is a dead end. Pop the corresponding index from the top of the stack.</li>

</ul>

where a neighbor is defined as a cell that is either horizontally or vertically next to reference cell. The last thing the makeMaze function should do before returning is reset the visited attribute of maze cells to false.

3.3      printMaze

This function will print a visual representation of the maze to the terminal. There are different ways that you can represent a maze, but one of the simplest is to use vertical bars | as vertical

<ol start="3">

 <li>MYMAZE</li>

</ol>

Figure 2: Path = True

borders, and dashes − − − as horizontal borders. You can use whatever characters you want, but make sure the output is reasonable. You can reference figure 1 as a good example.

If the path parameter is true, then you must print an asterisk ’∗’ in every cell where the visited attribute of the cell is true. Otherwise, if the path parameter is false, then do not print an asterisk ’∗’ in the center of the cell. The reason for this is so we can visualize the path that the printMaze() function took when solving the maze.

Figure 1 is what may be printed to the terminal for a maze of size 5×20 when the parameter path =false is passed in. Figure 2 is what is what may be printed to the terminal for a maze of size 5×20 when the parameter path=true is passed in.

You are not restricted to how you print off the maze, but it may be easiest to print off the maze by going though each row one-at-a-time. There may be two special cases depending on how you implement the algorithm. You may need to remove the walls for the entrance and exit on the border of the maze separate from the loop.

By the end of this function, you should have printed the entire representation of the maze. Do <strong>not </strong>reset the visited attribute of the cells.

3.4      solveMaze

To solve a maze, we will use a queue to test all possible paths. The algorithm should work as follows.:

<ul>

 <li>Initialize a queue with the start index {0, 0}</li>

 <li>Loop until the queue is empty:</li>

</ul>

<strong>– </strong>Dequeue the front index of the queue and mark the corresponding cell’s visited attribute as true.

<ol start="4">

 <li>GRADING RUBRIC

  <ul>

   <li>If the current cell is the finish point (i.e. the index {rows-1, columns-1}), then break.</li>

  </ul></li>

</ol>

The maze has been solved.

<ul>

 <li>Enqueue all reachable neighbors that are un-visited.</li>

</ul>

At the end of the function, call the printMaze function with path=true. An example of a solved maze is figure 2.

3.5      Testing

You are free to do any testing you see fit. You will know the functions are being generated correctly if there exists a path from the entrance cell to every cell of the maze, including the exit cell.