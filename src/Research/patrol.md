# Patrol Robot Research
## Project Structure 
In order to get the patrol simulation going, you need to type: 

```
roslaunch turtlebot_sim multi_patrol.launch
```

What this does is launch 8 `proj3_randGoal_patrol.launch` robots (disused below), Turtlebot_multi.rviz, the topology_patrol_generator from the go2goal package, the position rebroadcaster (so the turtlebots know the location of each other), as well as a network emulator node (figure out what this does).

### `proj3_randGoal_patrol`
This file contains the launching information to bring up `proj3_patrol.launch` (discussed below). It also loads up the random goal generator.

### proj3_patrol
This file is (finally) the one that brings up the turtlebot. This is what loads Rviz, creates the vehicle, and the go to goal node.

# Files to edit
## Go to Goal Control 
* `controllers/patrol_g2g/`
* `go2goal/topology_graph/`
* `go2goal/rand_goal_generator`
* `network_topology_emulator/delta_disk_emulator`
* `turtlebot_sim/simple_map_tf` 
