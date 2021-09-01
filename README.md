# pendulum-lstm
## Predicting Chaotic Double Pendulum with LSTMs
In this project, I aim to predict the trajectory of a chaotic double pendulum with machine learning techniques, in particular the LSTM (longshort-term memeory).
## Physics
The double pendulum is a simple dynamical system with one pendulum attached to the end of the other pendulum. Its trajectory is shown in Figure 1.

![alt text](https://upload.wikimedia.org/wikipedia/commons/6/65/Trajektorie_eines_Doppelpendels.gif)
Figure 1

By calculating the kinetic and potential energies of the system, we can construct the Lagrangian.

![alt text](https://wikimedia.org/api/rest_v1/media/math/render/svg/2ec151d95ac6e7eb0bb11dadf1c39dac6b9514f0)

Adopting a substitution of coordinates, the above equation becomes:

![alt text](https://user-images.githubusercontent.com/43424403/131668420-d726b42b-d655-485e-b563-68a8bc8becd3.png)

Applying the Euler-Lagrange equation, we can obtain the generalized momenta for the first and second masses.

![alt text](https://wikimedia.org/api/rest_v1/media/math/render/svg/d511d9e2eb6a41c02318bc469f6e94f7e2217f92)

Finally, inverting this equation gives us a coupled differential equation of the two masses, from where we can derive the trajectory of the system.

![alt text](https://wikimedia.org/api/rest_v1/media/math/render/svg/ea30dfe9ba779902cca5f518a71567407e4974ce)


## Method

Since this chaotic system is highly sensitive to intial conditions, I decided to use an LSTM approch, which solves the vanishing gradient problem in time-series studies, to predict the trajectory.

To obtain the training and testing data, I have used the Runge-Kutta approximation of the coupled differential equations. The training data are generated for 100 seconds with a step of 0.01, with intial angle displacement of 120 degrees.

The lookback is a single step, which means if the input is at time t, the netowrk predicts the position at time t+dt.

Using a 1:3 test-train split, a single hidden layer of 8 neurons connected to the output layer, MSE as the loss function, and the adam optimizer, the training took place for 50 epochs with a validation step of 30. As we can see from Figure 2, the training quickly converged. Two LSTMs were trained for the x and y coordinates independently.

<img width="323" alt="image" src="https://user-images.githubusercontent.com/43424403/131669642-b2f64e49-e64e-44e2-ac5a-a875299f96bf.png">
Figure 2

## Results

The results were quite surprising to me. The LSTMs were only trained on an intial displacement of 120 degrees, but the model was robust for all initial conditions, as can be seen below in Figures 3-6

<img width="582" alt="image" src="https://user-images.githubusercontent.com/43424403/131669986-ba40e43e-b51d-480c-ad15-5fa14fe415ff.png">
Figure 3: intial angle = 2
<img width="582" alt="image" src="https://user-images.githubusercontent.com/43424403/131670009-787b135e-db90-4335-bf3f-025124d8c214.png">
Figure 4: intial angle = 60
<img width="582" alt="image" src="https://user-images.githubusercontent.com/43424403/131670032-1b7e1484-84b6-4d35-abac-84158de368bf.png">
Figure 5: intial angle = 90
<img width="582" alt="image" src="https://user-images.githubusercontent.com/43424403/131670047-bb98965e-3526-47b1-a370-22b633348e7d.png">
Figure 6: intial angle = 180

The blue line shows the predicted trajectory and the red line shows the actual trajectory by interating the differential equations. The two paths agree quite well and never diverges.


