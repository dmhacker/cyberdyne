# Cyberdyne

This is an assortment of miscallenous neural network implementations, a collection that will be expanded on overtime. 

### Project Structure

```
cyberdyne
├── LICENSE
├── README.md
└── ti-84
    ├── NNET.8xp
    ├── NNETEXE.8xp
    ├── NNETGEN.8xp
    └── NNETLRN.8xp
```

### TI-84

Inside __ti-84/__ folder, there are 6 separate programs, each one handling a different aspect of a basic feed-forward neural network with tanh as the activation function. 

__NNET.8xp__ is the core program, and it contains the code for running the network given an appropriate input vector. The input and output vectors are stored in a TI-Basic lists, and the neuron/connection information is stored in a 2D matrix (TI-Basic does not support 3D matrices, so the information is flattened into a 2D one). 

__NNETEXE.8xp__ is a GUI wrapper around __NNET.8xp__. It allows the user to provide an input vector, and then the program calls __NNET.8xp__ to generate the output vector. The output vector is then printed, so the user can see.

__NNETGEN.8xp__ is used for generating the neural network. Every calculator can only hold one neural network (due to the number of matrices it requires), so this program will overwrite any previous network you have trained, unless its constituent weight matrix was backed up elsewhere. It takes in a list, with each integer in the list specifying how many neurons are that respective layer. e.g. {2, 3, 1} would create a three-layered network, with two inputs, one output, and one hidden layer with three neurons.

__NNETLRN.8xp__ is by far the bulkiest program of the four, mainly because it contains all the code for backpropogation. Users can control how many cycles to train the network for, what input-output pairs to train the network off (provided in a matrix), and what learning rate to use. The backpropogation algorithm it uses is standardized and widely used, but because the calculator takes so long to run backpropogation, especially when learning non-linearly-separable functions, I modified the algorithm with the usage of [the Fahlman constant](https://books.google.com/books?id=hY76AQAAQBAJ&pg=PA229&lpg=PA229&dq=fahlmans+constant&source=bl&ots=_bIsCr2hrl&sig=5p8JyE-Bov6kRi80h74ZN_4XqHU&hl=en&sa=X&ved=0ahUKEwiW3qG7safVAhVIr1QKHU2xDJ8Q6AEIMjAB#v=onepage&q=fahlmans%20constant&f=false), a small number (0.01) added to the derivative of the initial delta error. This has the effect of speeding up the network when the derivative of the error equals 0, commonly seen in the test case of the XOR function.

__NNETPLOT.8xp__ provides a nice visualization of the overall error of the network as you continue to train it. The error being plotted is the total sum squared error of the network, averaged across the entire training set. If the network is working correctly, you see an exponential decrease in error, and error should approach 0 (or close to 0) as the number of training cycles approaches infinity.

__NNETMAIN.8xp__ is the GUI portal program that links together __NNETEXE.8xp__, __NNETGEN.8xp__, __NNETLRN.8xp__, and __NNETPLOT.8xp__. It recommended you use this to start with access anything related to the neural network, rather than calling each of those programs individually from the EXEC screen.

