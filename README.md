# Hamiltonian-Neural-Networks
Make sure `numpy`, `matplotlib`, and `torch` are installed.
## List of Functions
- ``` L2_loss``` takes in two input vectors and calculates the mean squared error distance between the two vectors
- ``` hamiltonian_fn ``` function defines the Hamiltonian function that describes the dynamics of the system. This function is just used to generate the data set and is not used by the neural network. For now this function must only be used for single degree of freedom systems. In the future, we will modify the notebook to handle multiple degree of freedom systems. This function can be changed to define various single degree of freedom systems. 
- ``` dynamics_fn ``` This function calls ```hamiltonian_fn``` , finds its gradients and defines the Hamiltonian dynamical system
- ``` get_trajectory ``` calls ```dynamics_fn``` and uses ```scipy.integrate.solve_ivp``` to numerically integrate the dynamics starting from a specified initial condition
- ``` get_dataset ``` calls ```get_trajectory``` multiple times with various initial conditions based on the number of samples we require and generates a data set that can be used by the neural network to learn the Hamiltonian. This function aslo splits the data into training and testing sets.

## List of classes
- ``` MLP ``` class defines the multi layer perceptron (feedforward neural network) that takes in the generated data and predicts the Hamiltonian function
- ``` HNN ``` class defines the outer network for the ```MLP``` network. ```HNN``` calls ```MLP``` and finds the gradients of the Hamiltonian function. These gradients are used to find the loss with respect to the numerical derivatives calculated from the data.
 
## Working with the code
Modify the variable `dyn_sys` in the first line of the notebook to try out various dynamical systems the code can handle. Currently the code is built to handle a pendulum, a linear spring mass system and a nonlinear spring mass system.
```
'''
dyn_sys = 'pendulum' 
dyn_sys = 'linear_spring_mass'
dyn_sys = 'nonlinear_spring_mass'

are three valid values that the variable dyn_sys can take. 
Any other string throws an error as they are not defined.
Switch from one to the other to check the performance of the Hamiltonian Neural Network
on these two systems i.e., a spring mass system or a pendulum
'''
dyn_sys = 'nonlinear_spring_mass'
```


