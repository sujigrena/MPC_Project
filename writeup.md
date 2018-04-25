# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

---

I've implemented a Model Predictive Control for the driving the Udacity car simulator. This works by taking the planned path as the reference trajectory and by predicting the trajectory of motion using the current state during each step and there by taking correct action to reach the reference trajectory. Here we convert this into a optimization problem where we deal with calculating the low cost and smooth path in a given time step (we divide the entire path into small patches of time step for efficiency and accuracy).

### The Model:

The model takes into consider 6 states them being the position (x,y), the orientation (psi) , velocity (v), the cross track error and the error in orientation (cte and epsi). The two actuators we are controlling are the steer value and the throttle where +ve throttle means acceleration and -ve throttle means applying brake (delta , a). The update equations are based on a simple bicycle motion model.

### Time step and Elapsed time:
The final value for N and dt that I have considered are 10 and 0.05. I tried to run the simulator for value 25 and 0.1 and 20, 0.05. I found the pair (10,0.1) to run smoothly whereas the other two pair performed scarily (taking so many unnecessary turns and brakes) hence I selected 10 and 0.05 as my final value.

### Polynomial fitting:
I haven't performed any preprocessing for polynomial fitting of the reference trajectory. However, before passing the values of state I have taken the latency into account and have passed the states accordingly. The states were figured out by considering the `angle of the reference trajectory hasn't changed`.

### Dealing with Latency:
I have considered the movement of the car during the latency period (assuming as 0.1 second) and have updated my state with the new value. Therefore, when MPC calculates, it uses the values with the updated position based on Latency.