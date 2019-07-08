## !!! Under Construction !!!

# Calling Python Code / Script in Kafka Streams with Jep (TensorFlow Keras Example)

This project contains shows how to embed native Python code into a Kafka Streams application, e.g. to execute analytic models which are only available as Python source code.

The project uses [Jep (Java Embedded Python)](https://github.com/ninia/jep) and [Py4J (A Bridge between Python and Java)](https://www.py4j.org/). See the end of the README to learn more about different options.

## Machine Learning as Motivation for Integration of Python Source Code into a JVM Project

The Python Machine Learning ecosystem is huge.

With the recent surge of deep-learning, most of the established and stable libraries such as Keras/ Tensorflow / Theano are available in Python, and also provide (often limited or unstable) Java APIs. Thus, you can import analytic models trained with Python from a JVM application. This is ideal because data scientist can use their beloved Python while production engineers can easily integrate / import these models into mission-critical JVM-based applications.

However, often Python-native frameworks like scikit-learn are sufficient for many use cases and easier to use for the data scientist. Though, the output (i.e. ML algorythms or analytic models) is just Python code. It cannot be transformed into Java code or being important from Java applications easily. Therefore you need to execute Python code from Java applications somehow.

Let's take a look how to execute Python models from a real time streaming application built with Java, Apache Kafka, Kafka Streams and Jep.


### Example 1 - Python in Kafka Streams

#### Use Case - Kafka Streams and Py4J

Simple example using Kafka Streams and Py4J (thanks to Hubert Dulay).

This is the [Kafka Streams code (Scala)](https://github.com/hdulay/kstream-scala/blob/master/src/main/scala/example/LDAKStreamPy4j.scala).

This is the [Python code](https://github.com/hdulay/kstream-scala/blob/master/Model.py) which is called from the Kafka Streams application (just a hello world calculation, but be any Python ML function).

### Example 2 - Keras / TensorFlow in Kafka Streams

#### Use Case

Kafka Streams Python example

#### Machine Learning Technology

* [H2O](https://www.h2o.ai)
* Keras / TensorFlow
* TODO

## Jython vs. JyNI vs. Py4J vs. Jep for Java-Python Integration

I spent some time readig different websites, Stackoverflow discussions and (often several years old) blog posts. I only knew Jython and it is was my first thought for integration of Python with Java, but I learned a lot. Here I describe why this project uses Jep and Py4J:

* [Jython](http://www.jython.org/) is basically a re-implementation of python in Java. Although it does include most of the python modules, it lacks the support for C-Extension modules. Which essentially renders Jython useless for most of the libraries in the ML ecosystem as all of them use C-Extension to speedup the processing. I was really surprised to see that the last release of Jython was in May 2015.

* [JyNI (Jython Native Interface)](https://jyni.org/) is a compatibility layer with the goal to enable Jython to use native CPython extensions like NumPy or SciPy. However, JyNI doesn’t currently support the entire Python C-API, so it is not currently at a state where we can use it for libraries built using Cython.

* [Py4J (A Bridge between Python and Java)](https://www.py4j.org/) enables Python programs running in a Python interpreter to dynamically access Java objects in a Java Virtual Machine. This is the other way round and not helpful - we need to run Python from Java, not Java from Python. [UPDATE July 2019:] The docs are a little bit confusing. Actually, you can alos call Python from a Java class. The above Kafka Streams example uses Py4J therefore.

* [Jep: (Java Embeded Python)](https://github.com/ninia/jep) takes a different route and embeds CPython in Java using JNI. If you need to include CPython modules (such as numpy or other ML components), then Jep is the way to go.