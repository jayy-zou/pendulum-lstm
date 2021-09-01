# pendulum-lstm
## Predicting Chaotic Double Pendulum with LSTMs
In this project, I aim to predict the trajectory of a chaotic double pendulum with machine learning techniques, in particular the LSTM (long short-term memory).
## Physics
The double pendulum is a simple dynamical system with one pendulum attached to the end of the other pendulum. Its trajectory is shown in Figure 1.

![alt text](https://upload.wikimedia.org/wikipedia/commons/6/65/Trajektorie_eines_Doppelpendels.gif)
Figure 1

By calculating the kinetic and potential energies of the system, we can construct the Lagrangian.

<img width="504" alt="image" src="https://user-images.githubusercontent.com/43424403/131670894-041acb7f-c5b8-42b7-8fa3-fbe2966e1e8b.png">

Adopting a substitution of coordinates, the above equation becomes:

<img width="536" alt="image" src="https://user-images.githubusercontent.com/43424403/131670924-67297bdd-fc62-4c56-91aa-ad5df670bfa4.png">

Applying the Euler-Lagrange equation, we can obtain the generalized momenta for the first and second masses.

<img width="339" alt="image" src="https://user-images.githubusercontent.com/43424403/131670940-8205d4e2-8c6a-4b33-a4e2-0b5cf952dcef.png">

Finally, inverting this equation gives us a coupled differential equation of the two masses, from where we can derive the trajectory of the system.

<img width="265" alt="image" src="https://user-images.githubusercontent.com/43424403/131670962-09f84e09-59cb-4784-9efd-80affde8f174.png">

## Method

Since this chaotic system is highly sensitive to initial conditions, I decided to use an LSTM approach, which solves the vanishing gradient problem in time-series studies, to predict the trajectory.

To obtain the training and testing data, I have used the Runge-Kutta approximation of the coupled differential equations. The training data are generated for 100 seconds with a step of 0.01, with initial angle displacement of 120 degrees.

The lookback is a single step, which means if the input is at time t, the network predicts the position at time t+dt.

Using a 1:3 test-train split, a single hidden layer of 8 neurons connected to the output layer, MSE as the loss function, and the Adam optimizer, the training took place for 50 epochs with a validation step of 30. As we can see from Figure 2, the training quickly converged. Two LSTMs were trained for the x and y coordinates independently.

<img width="323" alt="image" src="https://user-images.githubusercontent.com/43424403/131669642-b2f64e49-e64e-44e2-ac5a-a875299f96bf.png">
Figure 2

## Results

The results were quite surprising to me. The LSTMs were only trained on an initial displacement of 120 degrees, but the model was robust for all initial conditions, as can be seen below in Figures 3-6

<img width="582" alt="image" src="https://user-images.githubusercontent.com/43424403/131669986-ba40e43e-b51d-480c-ad15-5fa14fe415ff.png">
Figure 3: intial angle = 2
<img width="582" alt="image" src="https://user-images.githubusercontent.com/43424403/131670009-787b135e-db90-4335-bf3f-025124d8c214.png">
Figure 4: intial angle = 60
<img width="582" alt="image" src="https://user-images.githubusercontent.com/43424403/131670032-1b7e1484-84b6-4d35-abac-84158de368bf.png">
Figure 5: intial angle = 90
<img width="582" alt="image" src="https://user-images.githubusercontent.com/43424403/131670047-bb98965e-3526-47b1-a370-22b633348e7d.png">
Figure 6: intial angle = 180


The blue line shows the predicted trajectory and the red line shows the actual trajectory by iterating the differential equations. The two paths agree quite well and never diverges.

## Discussion

This project has shown that an LSTM approach works well with the chaotic double-pendulum system. Even with a very simple network setup, the results converged quick and are robust to different initial conditions.

Future work could be done by training on multiple initial conditions, using more sophisticated LSTMs, finetuning hyperparameters, and applying physical constraints to the model. Additionally, a similar approach should be attempted on different chaotic systems; for example, the Rössler system, encryption and decryption, and weather systems (Figure 7).

<img width="271" alt="image" src="https://user-images.githubusercontent.com/43424403/131670783-a868990d-ad22-4218-9f76-51fda9741c0a.png">
