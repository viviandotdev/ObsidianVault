---
created: 2023-11-29 05:58
modified: 2025-06-15T06:57:35-04:00

---
tags:: [[neural-networks]]
source:: [The spelled-out intro to neural networks and backpropagation: building micrograd - YouTube](https://www.youtube.com/watch?v=VMj-3S1tku0)

### The spelled-out intro to neural networks and back propagation

### What is the difference between gradient and derivative?
The **derivative** focuses on the rate of change of a **function** with respect to a **single** variable, the **gradient** encompasses the rate of change of a **multivariable function** with respect to **all of its variables simultaneously.**
**The gradient gives us some power because we know how to influence the final outcome, this will extremely useful for training knowledge**

**Understanding Derivatives in Context of Function Slopes**
Derivatives tell us how **changing the inputs** will **affect** the **output** of the function.

```
L = d * f
dL/dd = f = derivative of L with respect to d
(f(x + h) - f(x)) / h = definition of a derivative
((d + h) * f) - d * f) / h
df + (hf - df) / h
hf / h
f
```
This means if we slightly increase the value of **d** by a small amount lets say **Δd** the corresponding change in the output function **ΔL** will be approximately **f × Δd**

### Neuron as an mathematical expression
**Neural Networks at a just a class of mathematical expression** that takes in inputs and weights and outputs a loss function or predictions

### Neural Networks High Level Steps
**Forward Pass**
The input data is fed through the neural network and each neuron's output is computed through a series of weighted sums and activations function to compute the "loss" function L.
**Back-propagation**
The derivative of the loss function with respect to each **weight** in the network is computed. This derivative is also known as the gradient, each weight in the neuron will have a derivative. This derivative will inform the network how to update the weights in the next step.
**Update the weights**
we can iteratively make these adjustments to get the output we want
The weights are adjusted in the opposite direction of the gradient, aiming to minimize the loss function.


### Implementing Neurons, Layers, and Multi-Layer Perceptrons in Code

```python
class Neuron:
  def __init__(self, nin):
    self.w = [Value(random.uniform(-1,1)) for _ in range(nin)]
    self.b = Value(random.uniform(-1,1))

  def __call__(self, x):
    # w * x + b, computes the output of the neuron
    act = sum((wi*xi for wi, xi in zip(self.w, x)), self.b)
    out = act.tanh()
    return out

  def parameters(self):
    return self.w + [self.b]
```

### Parts of Artificial Neuron
**Input Integration**- The neuron takes in the inputs and computes the weighted sum of the inputs
	**Inputs** are values feed into the network and they represent features of the data you want to process. These values remain **fixed** as the data propagates through the network.
	**Weights**- are parameters of the neural network and control the strength of connections between neurons in different layers. These weights are iteratively **adjusted** through back propagation to minimize the loss function.
**[[Activation Function]]**- mathematical function applied to the input of each neuron that introducing non-linearity.
**Output**- Once the activation function is applied the output of the neuron is transmitted to the neurons in the next layer.

![[Screenshot 2024-02-25 at 6.54.07 AM.png]]


```python
# List of neurons
class Layer:

  def __init__(self, nin, nout):
    self.neurons = [Neuron(nin) for _ in range(nout)]

  def __call__(self, x):
    outs = [n(x) for n in self.neurons]
    return outs[0] if len(outs) == 1 else outs

  def parameters(self):
    return [p for neuron in self.neurons for p in neuron.parameters()]
```

``` python
# List of layers
class MLP:

  def __init__(self, nin, nouts):
    sz = [nin] + nouts
    self.layers = [Layer(sz[i], sz[i+1]) for i in range(len(nouts))]

  def __call__(self, x):
    for layer in self.layers:
      x = layer(x)
    return x

  def parameters(self):
    return [p for layer in self.layers for p in layer.parameters()]
```
![[Screenshot 2024-02-25 at 7.39.24 AM.png]]

``` python
x = [2.0, 3.0, -1.0]
n = MLP(3, [4, 4, 1]) # create MLP with 1 input layer with 3 neurons, 2 hidden layers with 4 neurons and 1 output layer with one neuron.
n(x)
```


``` python
xs = [
  [2.0, 3.0, -1.0],
  [3.0, -1.0, 0.5],
  [0.5, 1.0, 1.0],
  [1.0, 1.0, -1.0],
]
ys = [1.0, -1.0, -1.0, 1.0] # desired targets


for k in range(20):
	# forward pass
	ypred = [n(x) for x in xs]
	loss = sum((yout - ygt)**2 for ygt, yout in zip(ys, ypred))
	# backward pass
	for p in n.parameters():
		p.grad = 0.0
	loss.backward() #compute the derivatives of each parameter with respect to the loss function.

	# update
	for p in n.parameters():
		p.data += -0.1 * p.grad print(k, loss.data)
	print(k, loss.data)
```


### Additional Resources
[nn-zero-to-[nn-zero-to-hero/lectures/micrograd at master · karpathy/nn-zero-to-hero · GitHub](https://github.com/karpathy/nn-zero-to-hero/tree/master/lectures/micrograd)
