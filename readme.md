## !!! Under Construction !!!

# Calling Python Code / Script in Kafka Streams with Jep (TensorFlow Keras Example)

This project contains shows how to embed native Python code into a Kafka Streams application, e.g. to execute analytic models which are only available as Python source code.

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

Simple Python example

#### Machine Learning Technology

* [H2O](https://www.h2o.ai)
* Keras / TensorFlow
* TODO