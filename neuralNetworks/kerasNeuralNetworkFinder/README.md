# Keras Neural Finder

To find the best neural network configuration. 

## Approach

Though Gridsearch can be used to fine tune most of the parameters, for some reason, unable to pass the neural layer/neuron count as parameter. Hence have come up with a custom implementation similar to GridSearch

## Usage

Define the list of hyper parameters as a dictionary in below format. 
While all the parameters are self-explanatory, the key parameter is the number of hidden layers & number of neurons in each layer. 

This can be defined in attribute number_of_neurons_in_hidden_layers in 2 ways. 

### Static List 

Define as a list containing a list of values. Each list denotes the number of layers and in turn the number of neurons as well in each layer 

```
[[11, 8, 6], [8, 6]]

1st Option - [11, 8, 6] - 3 Hidden layers with 11/8/6 neurons in each hidden layer
2nd Option - [8, 6] - 2 Hidden layers with 8/6 neurons in each hidden layer
```

### Range of Layers/Neuron combinations
This would help us give a range of # of numbers of layers to be tried with a range of neuron count as well


```
getLayerOptions({1:(8, 10), 2:(8, 10), 3:(6, 8)})


The parameter for this would be a dictionary in below. 

Ex: {1:(8, 13), 2:(5, 13), 3:(5, 8), 4:(5,6)}

Key -> Layer_number 
Values -> Tuple denoting the minimum and maximum number of neurons in that layer

Output of this will be [[8], [5], [3], [8,5], [8,3], [5,3]..]
```

```
hp_params = {}
hp_params['number_of_neurons_in_hidden_layers'] = getLayerOptions({1:(8, 10), 2:(8, 10), 3:(6, 8)})
hp_params['activation_fn_for_hidden_layers'] = ['sigmoid']
hp_params['activation_fn_for_output_layers'] = ['sigmoid']
hp_params['optimizers'] = [ 'Adam', 'Adamax']
hp_params['number_of_epochs'] = 10
hp_params['learning_rate_range'] = [0.1]
hp_params['w_initializer'] =  ['glorot_normal']
hp_params['b_initializer'] =  ['glorot_normal']
```

