# PRM
# 2D Probabilistic Roadmap Planner

This project implements a 2D Probabilistic Roadmap (PRM) planner, a path planning algorithm commonly used in robotics. The algorithm constructs a roadmap of possible paths in a given environment by randomly sampling points in the free space and connecting these points to form a graph. The resulting graph can then be used to find a collision-free path between a start and a goal position.

## Features

- **Environment Representation**: The workspace is represented as a 2D grid with obstacles.
- **Random Sampling**: Generates random nodes within the free space of the environment. I first used uniform random sampling. For those nodes (coordinate points) which collided with the obstacle, I used OBPRM (obstacle based probabilistic road-map). OBPRM is a method to find nodes close to the edge of an obstacle. It also helps create connections in narrow passages that may form between obstacles.
  
- Psuedocode is as follows :
  - node<sub>in</sub> found in collision (node in/ colliding with obstacle)
  - Generate random direction v (I chose from six possible directions, rotating by 60 degrees about the x_axis)
  - Find node<sub>out</sub> in direction v that is in  C<sub>free</sub> (done by 'moving' node<sub>in</sub> by a 'unit' amount along direction v.

    'unit' was chosen to be 0.05*max(width ,heigth) (where width and height refer to x_max and y_max of the C<sub>space</sub>).

    unit increases exponentially by a power of 2 to quickly find node<sub>out</sub>
  - Binary search between node<sub>in</sub> and node<sub>out</sub> till node closest to boundary and in C<sub>free</sub> is found

- **Node Connection**: Connects nodes to its 'n' closest nodes that it is not already connected to. all created edges are valid, meaning that they do not pass thorugh any obstacles.
  They were validated by finding the line equations for the edge and the obstacles' borders. Linear algebra was hten used to see if the lines intersected and if yes, whether the point of intersection lay on the line segment that created the edge. 
- **Pathfinding**: Utilizes A* algorithm, using greedy approach where the heuristic function is the euclidean distance between the currrent node and the goal and the cost is the distance from the start node to the current node.
The path found using A* is then shortened by removing intermediate unnecessary nodes. The distance saved is displayed.
- **Visualization**: Displays the roadmap, obstacles, and the computed path using Pylab.

## Getting Started

### Prerequisites

- Python 3.10+
- Required Python packages:
  - `numpy`
  - `pylab`

You can install the required packages using `pip`

- download the ipynb file and run all cells
- play around with the variables in the last cell (testing improvement cell) to see the path found in various environment and query confirgurations. 

