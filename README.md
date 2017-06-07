# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

---

## PID for steering and speed control

The implementation uses a PID controller for calculating the steering angle. In addition a speed control was implemented. In essence the speed control has 3 aims: 
* On a straight line accelerate as much as possible
* In a curve, reduce the speed
* If steering angle is over a certain limit, reduce speed
* enforce a minimum and maximum speed.

This functionality is done in the code in the method PID::GetThrottle()
There is of course room for optimization via fine-tuning the parameter values.


## Describe the effect each of the P, I, D components had in your implementation.

Student describes the effect of the P, I, D component of the PID algorithm in their implementation. Is it what you expected?

The calculation of the new steering angle happens in line 84 of file PID.cpp. Two of the three components have hard coded values. 

Component P: This parameters used to calculate the steering angle as a multiple of the current cross track error. If used as only component, it leads to heavy over-steering and oscillation around the desired steering angle. Therefore, further parameters are needed. 

Component D: This component is used to calculate the steering angle based on the difference of the cross track error of t1 relative to t0. By using this parameter, we reduce the oscillation that component P causes and ensure that the car drives at the end drives on a straight line. 

Component I: If we use only component P and D then the steering is only satisfactory if there is no systematic error in the steering. This could be for example a sensor error or a mechanical error that introduces a constant error. The result is that the car is driving in the right direction but in parallel to the desired line. In order to mitigate this we need to track the cumulative cross track error and use a way to reduce this cumulative error. 

## Describe how the final hyperparameters were chosen.

Initially I used twiddle to optimize all three parameters P, I,  D. I arrived at a solution that worked, but did not lead to higher speeds on the track. Waht I observed was that the Twiddle lead to values of parameter P and D of approximately 0.6. The car regularly over-steered. I then thought that it might be better to use Twiddle only for parameter I and set parameters P and D manually. The values were identified by experimenting and at the end they were set to P = 0.1 and D = 4.0. 

The car is still oscillating a bit around the ideal line, which indicates that the parameters should be further optimized.  

The I parameters was chosen by Twiddle() and the result is that the total error is close to zero. 



