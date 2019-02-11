## !!! Under Construction !!!

# Calling Python Code / Script in Kafka Streams with Jep (TensorFlow Keras Example)

This project contains shows how to embed native Python code into a Kafka Streams application, e.g. to execute analytic models which are only available as Python source code.

The project uses [Jep (Java Embedded Python)](https://github.com/ninia/jep). The end of the readme describe why Jep is used, and not other Java-Python integration alternatives like Jython, JyNi or Py4J.

## Machine Learning as Motivation for Integration of Python Source Code into a JVM Project

The Python Machine Learning ecosystem is huge.

With the recent surge of deep-learning, most of the established and stable libraries such as Keras/ Tensorflow / Theano are available in Python, and also provide (often limited or unstable) Java APIs. Thus, you can import analytic models trained with Python from a JVM application. This is ideal because data scientist can use their beloved Python while production engineers can easily integrate / import these models into mission-critical JVM-based applications.

However, often Python-native frameworks like scikit-learn are sufficient for many use cases and easier to use for the data scientist. Though, the output (i.e. ML algorythms or analytic models) is just Python code. It cannot be transformed into Java code or being important from Java applications easily. Therefore you need to execute Python code from Java applications somehow.

Let's take a look how to execute Python models from a real time streaming application built with Java, Apache Kafka, Kafka Streams and Jep.

## Requirements, Installation and Usage

The code is developed and tested on Mac and Linux operating systems. As Kafka does not support and work well on Windows, this is not tested at all.

Java 8 and Maven 3 are required. Maven will download all required dependencies.

Just download the project and run

                mvn clean package

Apache Kafka 2.1 is currently used. The code is also compatible with Kafka and Kafka Streams 1.1 and 2.0.

**Please make sure to run the Maven build without any changes first.** If it works without errors, you can change library versions, Java version, etc. and see if it still works or if you need to adjust code.

Every examples includes an implementation and an unit test. The examples are very simple and lightweight. No further configuration is needed to build and run it. Though, for this reason, the generated models are also included (and increase the download size of the project).

The unit tests use some Kafka helper classes like EmbeddedSingleNodeKafkaCluster in package **com.github.megachucky.kafka.streams.machinelearning.test.utils** so that you can run it without any other configuration or Kafka setup. 
If you want to run an implementation of a main class in package **com.github.megachucky.kafka.streams.machinelearning**, you need to start a Kafka cluster (with at least one Zookeeper and one Kafka broker running) and also create the required topics. So check out the unit tests first.

### Example 1 - Python in Kafka Streams

#### Use Case

Simple Python example

### Example 2 - Keras / TensorFlow in Kafka Streams

#### Use Case

Kafka Streams Python example

#### Machine Learning Technology

* [H2O](https://www.h2o.ai)
* Keras / TensorFlow
* TODO

## Jython vs. JyNI vs. Py4J vs. Jep for Java-Python Integration

Why this project uses Jep (Java Embedded Python):

* Jython is basically a re-implementation of python in Java. Although it does include most of the python modules, it lacks the support for C-Extension modules. Which essentially renders Jython useless for most of the libraries in the ML ecosystem as all of them use C-Extension to speedup the processing.

* JyNI (Jython Native Interface) is a compatibility layer with the goal to enable Jython to use native CPython extensions like NumPy or SciPy. However, JyNI doesn’t currently support the entire Python C-API, so it is not currently at a state where we can use it for libraries built using Cython.

* Py4J (A Bridge between Python and Java) enables Python programs running in a Python interpreter to dynamically access Java objects in a Java Virtual Machine. This is the other way round and not helpful - we need to run Python from Java, not Java from Python.

* Jep: (Java Embeded Python) Jep takes a different route and embeds CPython in Java using JNI. If you need to include CPython modules (such as numpy or other ML components), then Jep is the way to go.