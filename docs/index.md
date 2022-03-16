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

## Coding exercise: neurons in action



Now that we’ve seen that we can use a single neuron to solve the linear regression problem, go back to the minimizing loss Colab and see if you can spot how we were using neurons all along. Do you find this surprising? Did you figure it out the first time you saw the Colab? If so, what gave it away?

https://colab.research.google.com/github/tinyMLx/colabs/blob/master/2-2-3-MimimizingLoss.ipynb




## Coding exercise: multi-layer neural network

Now let’s explore the code from the previous reading through a Colab. You’ll be able to train both the single layer and multi-layer model described in the previous reading and explore their predictions and trained weights and biases. Which model learns faster? Which ends up making better predictions?

https://colab.research.google.com/github/tinyMLx/colabs/blob/master/2-2-5-FirstNeuralNetworkRevisited.ipynb



## Coding exercise: DNN

Now let’s explore the MNIST classification example through a Colab. You’ll get to train the model just described in the previous reading, learn how to inspect and analyze the various trained layers in the model, and test the final model on additional data sets!

https://colab.research.google.com/github/tinyMLx/colabs/blob/master/2-2-7-ExploringCategorical.ipynb



## Coding assignment

In this assignment we'll dive a little deeper with a series of hands on exercises to better understand DNN learning with Tensorflow.

Remember that if you are taking the class for a certificate we will be asking you questions about the assignment in the test!

https://colab.research.google.com/github/tinyMLx/colabs/blob/master/2-2-12-AssignmentQuestion.ipynb





Up to this point you have learned the Machine Learning paradigm, and how it works to allow a computer to figure out the parameters that fit a function. When that function gives you the rules to map data to answers, you’ve changed from a programming paradigm where you have to figure out the rules that act on the data to give you answers:

Rules and data feed into traditional programming which then outputs answers.

To one that looks like this, where you provide the answers with the data, and the computer figures out the rules that maps them to each other:

Answers and data feed into machine learning and from this rules emerge.

To achieve this, of course, you still need to write code, but instead of writing the code for the rules, you write the code that figures out what the rules are. The algorithm to do this looks like the following:

Making a guess leads to measuring your accuracy which leads to optimizing your guess. This then gets repeated where you make a guess again and repeat the process. Arrows connect the steps.

As an example, you used two sets of numbers, for X and Y and wrote code that used the above algorithm to figure out the relationship between them where Y = wX+b, and the above algorithm could figure out the values of w and b that would fit.

This was the basis of a mathematical neuron, where the neuron could store the values of w and b, and again, using the above algorithm, those values could be figured out to give the desired Y for an input X.

An input of X is fed into a neuron and an out Y is created.

When these neurons are used together, in layers, more complex relationships could be figured out, and you saw how having multiple output neurons could take you into the territory of classification, where, each neuron could have a role in the final output, which of course is perfect for computer vision. Below is a simplified neural network diagram illustrating this point where input data can be classified -- i.e. does the network ‘see’ a dog or a cat.

An image of a cat’s face is fed into multiple neurons. Each of these neurons outputs a decision of whether the cat’s face represents a cat or a dog.

Basic neurons, stacked together like this form what is called a Dense layer, based on the fact that they’re densely connected to each other. When there are multiple layers between the input and the output, you have a Deep neural network, which gives us the term Deep Learning. Additionally, the layers between the input and the output are often called >hidden layers.

As you continue your Machine Learning journey, you’ll discover that there are many other types of layer that learn different parameters to just the w and b that a neuron learns.

For example, there are Recurrent layers, that are beyond the scope of this course, but they are able to learn values in a sequence where each neuron learns values and passes those values to another neuron in the same layer. The basic idea can be represented like this:

Recurrent layers are represented by having each layer indexed by a subscript. Here there is x zero x one and x two. On the outputs there is y zero y one and y two.

Where, if we have a sequence of values, X0, X1, X2 that we want to learn a corresponding sequence Y0, Y1, Y2 for, then the idea is the the neurons (F) can not only try to match X0->Y0, but also pass values along the sequence, indicated by the right pointing arrows, so the input to the second neuron is the output from the first and X1, from which it can learn the parameters for Y1 and so on.

There are many variations on this idea, but a very powerful one is called Long Short Term Memory where not only are values passed from neuron to neuron, so that X0 can impact Y1, X1 can impact Y2, but values from further back can also have an impact -- so that X0 could impact Y99 for example. This is achieved using a data structure called a Cell State where context can be preserved across multiple neurons.

Recurrent layers are represented by having each layer indexed by a subscript. Here there is x zero x one and x two. On the outputs there is y zero y one and y two.

Another type of neural network layer is called a Convolution, where a filter that can transform data, particularly image data, can be learned. You’ll explore those next!

I hope this helps you understand that Machine Learning goes beyond simple neurons that learn a w and b in the Y=wX+b scenario.






## Coding exercise: filters


In this Colab you’ll explore how filters and convolutions can be used to extract features from images. You’ll see firsthand how different filters can extract different features. You’ll also learn about pooling and explore how it can help reduce the amount of information while retaining important features. Click the link to get started!

https://colab.research.google.com/github/tinyMLx/colabs/blob/master/2-3-3-ExploringConvolutions.ipynb



## Coding exercise: CNN
In this Colab you’ll explore the power of Convolutional Neural Networks (CNNs). You’ll train both a traditional DNN and a CNN and see how CNNs can far outperform standard networks on computer vision tasks. You’ll then dive into both the convolutional and max pooling layers that power the CNN.

https://colab.research.google.com/github/tinyMLx/colabs/blob/master/2-3-5-FashionMNISTConvolutions.ipynb





## Coding exercise: computer vision
In this Colab you’ll build off of the prior Colab exercise using CNNs to learn the Fashion MNIST dataset, and you’ll start to visualize the convolution and pooling layers to better understand how the model “sees” the world. Hopefully this will give you more insight into how neural networks see the world as compared to how you see the world!

https://colab.research.google.com/github/tinyMLx/colabs/blob/master/2-3-7-FashionMNISTConvolutionsVisualizations.ipynb



## Coding exercise: complex images

In this Colab you’ll get to explore hands on the concepts discussed in the previous video. You’ll start by downloading and organizing the horses v. humans image database using Generators. You’ll then train a model using your organized data and then get to upload your own horse or human image and see if the model can detect it correctly. Finally you’ll get to visualize the model layers.

Note: as many learners have pointed out in the discussion below, the final model will only work well on images that are similar to those in our limited example dataset. As such, do not be surprised if you can trick the model!

https://colab.research.google.com/github/tinyMLx/colabs/blob/master/2-4-3-HorsesOrHumans.ipynb





## Coding exercise: Image Augmentation



In this Colab, we’ll again explore the horses v. humans Colab. This time, however, we will train with all forms of data augmentation turned on. You’ll see how this generates quite a bit more data (which takes longer to train) but produces a much more generalizable model since we are avoiding overfitting. You’ll get to test this by again having the chance to upload your own horse or human image and see if the model can detect it correctly. Finally you’ll again get to visualize the model layers.

As many students have noted in the discussion forum, since we are training on a very limited dataset, with a very small model, the final model does make a decent amount of mistakes. You'll find that if you test with images that look closer to the training dataset it will work much better. This is because while we are avoiding some overfitting with data augmentation, all machine learning models will struggle to generalize far beyond the training dataset!

https://colab.research.google.com/github/tinyMLx/colabs/blob/master/2-4-6-HorseOrHumanWithAugmentation.ipynb