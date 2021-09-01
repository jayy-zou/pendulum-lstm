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


## Under Construction
