# Node Voltage Method
The node voltage method is based off KCL.

## Definition: node voltage
When the term node voltage is used, we are referring to the potential difference between two nodes of a circuit. 

![Node_Voltage](https://ka-perseus-images.s3.amazonaws.com/8554e9d029ef653544153d3eb1d5b975bcafb01a.svg)

We select one of the nodes (as shown in the image above) to be the reference node. All other nodes voltages are measured with respect to the one reference node. For example, if node c is assigned as the reference node, we establish two node voltages at nodes a and b. The potential of the ground node (reference node) is defined to be 0 V.

## Node Voltage Method
* Assign a reference node
* Assign node voltage names to the remaining nodes
* Solve the easy nodes first, the ones with a voltage source connected to the reference node.
* Write KCL for each node. Do Ohm's Law in your head. 
* Solve the resulting system of equations for all node voltages. 
* Solve for any currents you want to know using Ohm's Law. 

### Assign a reference node and node voltages
Lets look at another example of setting a refernce node. Take the image below for example:

![Example2](https://ka-perseus-images.s3.amazonaws.com/c65c20dc1b1dd1b122da9d069c20e2112633c929.svg)

A good place is node c because it has a lot of connections and connects to both sources. 

### Node voltages control the current arrow
**The node voltages control the direction of the current arrow**.

Looking at the schematic below:

![direction_of_current](https://ka-perseus-images.s3.amazonaws.com/feae0d74b3bfa636a2c47e5bee04626fe273c3cc.svg)

The voltage that is more positive will be the first term of the equation.

## Solve the easy nodes
In the schematic:

![easy_nodes](https://ka-perseus-images.s3.amazonaws.com/ae623711418ff70b2c21dac0286032a4e59e858a.svg)

Node a is easy to solve, $V_a = 140\; V$

### Third important Node Voltage skill - do Ohm's Law in your head as your write KCL
We now write a KCL equation for the remaining unsolved node, b. Node voltage $v_b$ is the independent variable. So we can then write for the $20 \ohm$ resistor:

$$
\frac{140-v_b}{20}
$$

The current in the $6 \ohm$ and $5 \ohm$ resistors instantly goes into the equations as $-\frac{v_b}{6}$ and $- \frac{v_b}{5}$. This leaves us with the equation:

$$
\frac{140-v_b}{20} - \frac{-v_b}{6} - \frac{v_b}{5}
$$

## Find the node voltages
From this we can solve for $v_b$ directly.

## Solve for unknown currents using Ohm's Law
We now know all the voltages, we can then solve for currents at each location.

# Guided Example
Solve the circuit using the node voltage method

![guided_example](https://ka-perseus-images.s3.amazonaws.com/52b04fe26c007ea74c2151a7041df1ffa31d9866.svg)

1. Assign a reference node
  * The node at the very bottom is a good choice because it has 3 connections and it connects to the negative terminal of the voltage source.
2. Assign node voltage names to the remaining nodes
  * There are three other nodes. These are shown in the schematic below

![node_names](https://ka-perseus-images.s3.amazonaws.com/92f099da34ac10e4df2733aee0bde01c93a1fce4.svg)

3. The voltage in node a has to be $75 V$. 
4. It is useful to draw the direction of the currents. Keep in mind that current is flowing from high voltage to low voltage regions. This will keep track of direction of flow. Knowing if flow is going in or out of the node will make it easy to solve KCL at each node.

![KVL_guide](https://ka-perseus-images.s3.amazonaws.com/6b2e0dc07f24fbbcd6f1cb2e38061f1b4e214c1c.svg)

This leaves us with the equations:

**Node B**
$$
\frac{v_a - v_b}{25} - \frac{v_b}{50} + \frac{v_b - v_c}{10} = 0
$$

**Node C**
$$
\frac{v_a - v_c}{100} + \frac{v_b - v_c}{10} - \frac{v_c}{25}
$$

5. Solve the resulting system of equations for all node voltages
    Solving the system of equations we just created, we find that v_b = 37.5; V and v_c = 30$. 