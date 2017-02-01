Khronus Integration    ![Build Status](https://travis-ci.org/kamon-io/kamon-khronus.svg?branch=master)
==========================

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/kamon-io/Kamon?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/io.kamon/kamon-khronus_2.11/badge.svg)](https://maven-badges.herokuapp.com/maven-central/io.kamon/kamon-khronus_2.11)

Reporting Metrics to Khronus
============================

[Khronus] is an open source, distributed and reactive time series database designed to store, retrieve, analyze and process a large amount of custom metrics.

### Getting Started

Kamon khronus module is currently available for Scala 2.10, 2.11 and 2.12.

Supported releases and dependencies are shown below.

| kamon-khronus  | status | jdk  | scala            | akka   |
|:------:|:------:|:----:|------------------|:------:|
|  0.6.5 | stable | 1.7+, 1.8+ | 2.10, 2.11, 2.12  | 2.3.x, 2.4.x |

To get started with SBT, simply add the following to your `build.sbt`
file:

```scala
libraryDependencies += "io.kamon" %% "kamon-khronus" % "0.6.5"
```
Configuration
-------------

Set `kamon.khronus.host` to point to your Khronus instance using a `host:port` value like `11.22.33.44:1173`. Most likely, you will also want to set `kamon.khronus.app-name` to the application name you wish to report metric as.

These are the configuration keys available and their default values (taken from the `reference.conf` file supplied with this module):

``` typesafeconfig 
kamon {
  khronus {
    host = "127.0.0.1:1173"
    app-name = "kamon-khronus"
    # Time interval in milliseconds to flush the buffer and send the accumulated metrics.
    # It must be less than the smallest time window configured in Khronus.
    interval = 3000
    # Maximum number of measures to hold in memory within intervals.
    # Past this threshold, metrics will be discarded.
    max-measures = 500000
  }
}
```

Reported Metrics
----------------

This reporter will automatically subscribe itself to the following categories:

* __counter__.
* __histogram__.
* __gauge__.
* __trace__.
* __executor-service__.

The other important categories like __akka-*__, __system-metrics__, and __http-server__ were not included in this initial version due to time constraints. Also, there are no facilities for filtering categories. Please feel free to jump in!

[Khronus]: https://github.com/Searchlight/khronus
