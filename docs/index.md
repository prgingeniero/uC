#
<center>
    <h1 style="color:Orange;">Programacion</h1>
</center>
https://learning.edx.org/course/course-v1:HarvardX+TinyML1+3T2020/home



# Fundamentals of TinyML



As mentioned earlier, we’ll be using the Colab environment for much of our programming in this specialization.  In order to ensure that everyone has some hands on experience with  Colab, please follow the link below to Google’s Introductory Colab. In  it they provide a handful of quick tips and hands on exercises to get  you started using the Colab environment.

https://colab.research.google.com/notebooks/intro.ipynb


For machine learning in this course we are going to use Google’s TensorFlow Machine Learning framework. TensorFlow is widely used across industry and academia. To get you started with TensorFlow here is Google’s wonderful intro to TensorFlow video.



# Sample TensorFlow code

While TensorFlow is written with fast custom C++ code under the hood, it has a high level Python interface that we will use throughout this course. As such, you’ll need to be comfortable with basic coding in Python for this course.

For example we might create a custom Neural Network model using code that looks something like the below. Don’t worry if you don’t know what all of the words mean, we’ll walk you through all of these topics later in the course. For now just make sure you know enough Python to understand the following high level takeaways:

    This is a custom class that extends the tf.keras.Model base class
    It defines four specific kinds of tf.keras.layers
    It has a call function which will run an input through those layers (functions)

If that resonates with you then you probably know enough Python to do well in this course!

If you don’t feel like you know enough Python yet, don’t worry. Both Python.org and LearnPython.org have great resources you can use to get you up to speed. We’re sure that with a little work, very soon you’ll be ready to proceed with this course.

# Load in the TensorFlow library

import tensorflow as tf

# Define my custom Neural Network model

class MyModel(tf.keras.Model):

    def __init__(self):

        super(MyModel, self).__init__()

        # define Neural Network layer types

        self.conv = tf.keras.layers.Conv2D(32, 3, activation='relu')

        self.flatten = tf.keras.layers.Flatten()

        self.dense1 = tf.keras.layers.Dense(128, activation='relu')

        self.dense2 = tf.keras.layers.Dense(10)

run my Neural Network model by evaluating

    # each layer on my input data

    def call(self, x):

        x = self.conv(x)

        x = self.flatten(x)

        x = self.dense1(x)

        x = self.dense2(x)

        return x

# Create an instance of the model

model = MyModel()


## Coding exercise

In this next Colab you will get to explore linear regression and loss functions for yourself. We have provided a cell that will compute the predicted Y values as well as the loss function for your guess of w and b. Simply change their values and explore how the output and loss changes.

Note: You may receive a warning that the Colab was not authored by Google, and this may occur on future Colabs as well. That is entirely normal as we authored many of these Colabs ourselves for this course

https://colab.research.google.com/github/tinyMLx/colabs/blob/master/2-1-4-ExploringLoss.ipynb


## Coding exercise: Gradient descent
In this next Colab you will get to minimize the loss function for our linear regression model using TensorFlow’s built-in GradientTape class. You will also get to visualize the training process, seeing how both the bias and weight converge on the optimal solution across training epochs.

https://colab.research.google.com/github/tinyMLx/colabs/blob/master/2-1-6-MimimizingLoss.ipynb


## Coding exercise: neural networks

In this next Colab you will get to explore training your first neural network—see just how easy that can be with TensorFlow. You’ll also see the result of the question posed at the end of the last video—will the predicted Y be 19 for X = 10? Launch the Colab to find out!

https://colab.research.google.com/github/tinyMLx/colabs/blob/master/2-1-9-FirstNeuralNetwork.ipynb




## More neural networks



Up to now you’ve been looking at matching X values to Y values when there’s a linear relationship between them. So, for example, you matched the X values in this set [-1, 0 , 1, 2, 3, 4] to the Y values in this set [-3, -1, 1, 3, 5, 7] by figuring out the equation Y=2X-1.

You then saw how a very simple neural network with a single neuron within it could be used for this.

An input leads into a neuron as an arrow. Out of this an output arrow is generated.

This worked very well, because, in reality, what is referred to as a ‘neuron’ here is simply a function that has two learnable parameters, called a ‘weight’ and a ‘bias’, where, the output of the neuron will be:

Output = (Weight * Input) + Bias

So, for learning the linear relationship between our Xs and Ys, this maps perfectly, where we want the weight to be learned as ‘2’, and the bias as ‘-1’. In the code you saw this happening.

When multiple neurons work together in layers, the learned weights and biases across these layers can then have the effect of letting the neural network learn more complex patterns. You’ll learn more about how this works later in the course.

In your first Neural Network you saw neurons that were densely connected to each other, so you saw the Dense layer type. As well as neurons like this, there are also additional layer types in TensorFlow that you’ll encounter. Here’s just a few of them:

    Convolutional layers contain filters that can be used to transform data. The values of these filters will be learned in the same way as the parameters in the Dense neuron you saw here. Thus, a network containing them can learn how to transform data effectively. This is especially useful in Computer Vision, which you’ll see later in this course. We’ll even use these convolutional layers that are typically used for vision models to do speech detection! Are you wondering how or why? Stay tuned!
    Recurrent layers learn about the relationships between pieces of data in a sequence. There are many types of recurrent layer, with a popular one called LSTM (Long, Short Term Memory), being particularly effective. Recurrent layers are useful for predicting sequence data (like the weather), or understanding text.

You’ll also encounter layer types that don’t learn parameters themselves, but which can affect the other layers. These include layers like dropouts, which are used to reduce the density of connection between dense layers to make them more efficient, pooling which can be used to reduce the amount of data flowing through the network to remove unnecessary information, and lambda lambda layers that allow you to execute arbitrary code.

Your journey over the next few videos will primarily deal with the Dense network type, and you’ll start to explore how multiple layers can work together to infer the rules that match your data to your labels.


## Neural networks in action


You’ve now seen a very simple example for how computers can learn. There’s no great mystery to it -- it’s a simple algorithm of making a guess, measuring how good that guess is (aka the loss), and then using this information to optimize the guess, and continually repeating this process to improve the guess.

What you’ve seen -- fitting numbers in an equation -- might seem trivial, but the methodology that you used to do this is the same as is used in far more sophisticated scenarios.

To understand just how powerful this simple method - Machine Learning - can be, lets now explore a couple of new and exciting case studies:

The first is the story of a young woman, Nazrini Siraji who used Machine Learning to detect diseases in crops, helping to stem the destruction of crops in her home country of Uganda: https://www.youtube.com/watch?v=23Q7HciuVyM

Next, is air cognizer, built by undergraduate students in India, who realized that pictures of the sky, when matched to labels on air pollution could be used to build a new type of air quality sensor, using just the cameras on their phones: https://www.youtube.com/watch?v=9r2VVM4nfk8

Finally, here’s a talk from a Google engineer about how Google used images of retinas to build a diabetic retinopathy detector using TensorFlow that performs state of the art diagnosis of this disease: https://www.youtube.com/watch?v=oOeZ7IgEN4o
