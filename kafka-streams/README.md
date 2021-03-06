# Kafka Streams examples [![Build Status](https://travis-ci.org/confluentinc/examples.svg?branch=kafka-0.10.0.0-cp-3.0.0)](https://travis-ci.org/confluentinc/examples)

This sub-folder contains code examples that demonstrate how to implement real-time processing applications using Kafka
Streams, which is a new stream processing library included with the [Apache Kafka](http://kafka.apache.org/) open source
project.

---
Table of Contents

* [Available examples](#available-examples)
    * [Java](#examples-java)
    * [Scala](#examples-scala)
* [Requirements](#requirements)
    * [Apache Kafka](#requirements-kafka)
    * [Confluent Platform](#requirements-confluent-platform)
    * [Java](#requirements-java)
    * [Scala](#requirements-scala)
* [Packaging and running the examples](#packaging-and-running)
* [Development](#development)
* [Version Compatibility Matrix](#version-compatibility)

---


<a name="available-examples"/>

# Available examples

> Note: See [Version Compatibility Matrix](#version-compatibility) below for an overview of
> which examples are available for which versions of Apache Kafka and Confluent Platform.


<a name="examples-java"/>

## Java

> Note: We use the label "Lambda" to denote examples that make use of lambda expressions and thus require Java 8+.

* [WordCountLambdaExample](src/main/java/io/confluent/examples/streams/WordCountLambdaExample.java)
  -- demonstrates, using the Kafka Streams DSL, how to implement the WordCount program that computes a simple word
  occurrence histogram from an input text.
* [MapFunctionLambdaExample](src/main/java/io/confluent/examples/streams/MapFunctionLambdaExample.java)
  -- demonstrates how to perform stateless transformations via map functions, using the Kafka Streams DSL
  (see also the Scala variant
  [MapFunctionScalaExample](src/main/scala/io/confluent/examples/streams/MapFunctionScalaExample.scala))
* [SumLambdaExample](src/main/java/io/confluent/examples/streams/SumLambdaExample.java)
  -- demonstrates how to perform stateful transformations via `reduce`, using the Kafka Streams DSL
* [PageViewRegionLambdaExample](src/main/java/io/confluent/examples/streams/PageViewRegionLambdaExample.java)
  -- demonstrates how to perform a join between a `KStream` and a `KTable`, i.e. an example of a stateful computation
    * Variant: [PageViewRegionExample](src/main/java/io/confluent/examples/streams/PageViewRegionExample.java),
      which implements the same example but without lambda expressions and thus works with Java 7+.
* Working with data in Apache Avro format (see also the end-to-end demos under integration tests below):
    * Generic Avro:
      [PageViewRegionLambdaExample](src/main/java/io/confluent/examples/streams/PageViewRegionLambdaExample.java)
      (Java 8+) and
      [PageViewRegionExample](src/main/java/io/confluent/examples/streams/PageViewRegionExample.java) (Java 7+)
    * Specific Avro:
      [WikipediaFeedAvroLambdaExample](src/main/java/io/confluent/examples/streams/WikipediaFeedAvroLambdaExample.java)
      (Java 8+) and
      [WikipediaFeedAvroExample](src/main/java/io/confluent/examples/streams/WikipediaFeedAvroExample.java) (Java 7+)
* And [further examples](src/main/java/io/confluent/examples/streams/).

There are also a few **integration tests**, which demonstrate end-to-end data pipelines.  Here, we spawn embedded Kafka
clusters and the [Confluent Schema Registry](https://github.com/confluentinc/schema-registry), feed input data to them, process the data using Kafka Streams, and finally verify the output results.

> Tip: Run `mvn test` to launch the integration tests.

* [WordCountLambdaIntegrationTest](src/test/java/io/confluent/examples/streams/WordCountLambdaIntegrationTest.java)
* [JoinLambdaIntegrationTest](src/test/java/io/confluent/examples/streams/JoinLambdaIntegrationTest.java)
* [MapFunctionLambdaIntegrationTest](src/test/java/io/confluent/examples/streams/MapFunctionLambdaIntegrationTest.java)
* [PassThroughIntegrationTest](src/test/java/io/confluent/examples/streams/PassThroughIntegrationTest.java)
* [SumLambdaIntegrationTest](src/test/java/io/confluent/examples/streams/SumLambdaIntegrationTest.java)
* [GenericAvroIntegrationTest.java](src/test/java/io/confluent/examples/streams/GenericAvroIntegrationTest.java)
* [SpecificAvroIntegrationTest.java](src/test/java/io/confluent/examples/streams/SpecificAvroIntegrationTest.java)


<a name="examples-scala"/>

## Scala

* [MapFunctionScalaExample](src/main/scala/io/confluent/examples/streams/MapFunctionScalaExample.scala)
  -- demonstrates how to perform simple, state-less transformations via map functions, using the Kafka Streams DSL
  (see also the Java variant
  [MapFunctionLambdaExample](src/main/java/io/confluent/examples/streams/MapFunctionLambdaExample.java))

There is also an integration test, which demonstrates end-to-end data pipelines.  Here, we spawn embedded Kafka
clusters, feed input data to them, process the data using Kafka Streams, and finally verify the output results.

> Tip: Run `mvn test` to launch the integration tests.

* [JoinScalaIntegrationTest](src/test/scala/io/confluent/examples/streams/JoinScalaIntegrationTest.scala)


<a name="requirements"/>

# Requirements

<a name="requirements-kafka"/>

## Apache Kafka

The code in this repository requires Apache Kafka 0.10.0+ because from this point onwards Kafka includes its
[Kafka Streams](https://github.com/apache/kafka/tree/trunk/streams) library.


<a name="requirements-confluent-platform"/>

## Confluent Platform

The code in this repository requires Confluent Platform 3.0.x.

* [Confluent Platform 3.0.0 Quickstart](http://docs.confluent.io/3.0.0/quickstart.html) (how to download and install)
* [Confluent Platform 3.0.0 documentation](http://docs.confluent.io/3.0.0/)


<a name="requirements-java"/>

## Java 8

Some code examples require Java 8, primarily because of the usage of
[lambda expressions](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html).

IntelliJ IDEA users:

* Open _File > Project structure_
* Select "Project" on the left.
    * Set "Project SDK" to Java 1.8.
    * Set "Project language level" to "8 - Lambdas, type annotations, etc."


<a name="requirements-scala"/>

## Scala

> Scala is required only for the Scala examples in this repository.  If you are a Java developer you can safely ignore
> this section.

If you want to experiment with the Scala examples in this repository, you need a version of Scala that supports Java 8
and SAM / Java lambda (e.g. Scala 2.11 with * `-Xexperimental` compiler flag, or 2.12).


<a name="packaging-and-running"/>

# Packaging and running the examples

The first step is to install and run a Kafka cluster, which must consist of at least one Kafka broker as well as
at least one ZooKeeper instance.  Some examples may also require a running instance of Confluent schema registry.
The [Confluent Platform 3.0.0 Quickstart](http://docs.confluent.io/3.0.0/quickstart.html) guide provides the full
details.

In a nutshell:

```shell
# Start ZooKeeper
$ ./bin/zookeeper-server-start ./etc/kafka/zookeeper.properties

# In a separate terminal, start Kafka broker
$ ./bin/kafka-server-start ./etc/kafka/server.properties

# In a separate terminal, start Confluent schema registry
$ ./bin/schema-registry-start ./etc/schema-registry/schema-registry.properties

# Again, please refer to the Confluent Platform Quickstart for details such as
# how to download Confluent Platform, how to stop the above three services, etc.
```

> Tip:  You can also run `mvn test`, which executes the included integration tests.  These tests spawn embedded Kafka
> clusters to showcase the Kafka Streams functionality end-to-end.  The benefit of the integration tests is that you
> don't need to install and run a Kafka cluster yourself.

If you want to run the examples against a Kafka cluster, you may want to create a standalone jar ("fat jar") of the
Kafka Streams examples via:

```shell
# Create a standalone jar
#
# Tip: You can also disable the test suite (e.g. to speed up the packaging
#      or to lower JVM memory usage) if needed:
#
#     $ mvn -DskipTests=true clean package
#
$ mvn clean package

# >>> Creates target/streams-examples-3.1.0-SNAPSHOT-standalone.jar
```

You can now run the example applications as follows:

```shell
# Run an example application from the standalone jar.
# Here: `WordCountLambdaExample`
$ java -cp target/streams-examples-3.1.0-SNAPSHOT-standalone.jar \
  io.confluent.examples.streams.WordCountLambdaExample
```

Keep in mind that the machine on which you run the command above must have access to the Kafka/ZK clusters you
configured in the code examples.  By default, the code examples assume the Kafka cluster is accessible via
`localhost:9092` (Kafka broker) and the ZooKeeper ensemble via `localhost:2181`.


<a name="development"/>

# Development

This project uses the standard maven lifecycle and commands such as:

```shell
$ mvn compile # This also generates Java classes from the Avro schemas
$ mvn test    # But no tests yet!
```


<a name="version-compatibility"/>

# Version Compatibility Matrix

| Branch (this repo)                                                             | Apache Kafka      | Confluent Platform |
| -------------------------------------------------------------------------------|-------------------|--------------------|
| [master](../../../tree/master/kafka-streams)                                   | 0.10.1.0-SNAPSHOT | 3.0.0              |
| [kafka-0.10.0.0-cp-3.0.0](../../../tree/kafka-0.10.0.0-cp-3.0.0/kafka-streams) | 0.10.0.0(-cp1)    | 3.0.0              |

The `master` branch of this repository represents active development, and may require additional steps on your side to
make it compile.  Check this README as well as [pom.xml](pom.xml) for any such information.
