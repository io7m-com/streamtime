streamtime
===

[![Maven Central](https://img.shields.io/maven-central/v/com.io7m.streamtime/com.io7m.streamtime.svg?style=flat-square)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.io7m.streamtime%22)
[![Maven Central (snapshot)](https://img.shields.io/nexus/s/com.io7m.streamtime/com.io7m.streamtime?server=https%3A%2F%2Fs01.oss.sonatype.org&style=flat-square)](https://s01.oss.sonatype.org/content/repositories/snapshots/com/io7m/streamtime/)
[![Codecov](https://img.shields.io/codecov/c/github/io7m-com/streamtime.svg?style=flat-square)](https://codecov.io/gh/io7m-com/streamtime)
![Java Version](https://img.shields.io/badge/21-java?label=java&color=e6c35c)

![com.io7m.streamtime](./src/site/resources/streamtime.jpg?raw=true)

| JVM | Platform | Status |
|-----|----------|--------|
| OpenJDK (Temurin) Current | Linux | [![Build (OpenJDK (Temurin) Current, Linux)](https://img.shields.io/github/actions/workflow/status/io7m-com/streamtime/main.linux.temurin.current.yml)](https://www.github.com/io7m-com/streamtime/actions?query=workflow%3Amain.linux.temurin.current)|
| OpenJDK (Temurin) LTS | Linux | [![Build (OpenJDK (Temurin) LTS, Linux)](https://img.shields.io/github/actions/workflow/status/io7m-com/streamtime/main.linux.temurin.lts.yml)](https://www.github.com/io7m-com/streamtime/actions?query=workflow%3Amain.linux.temurin.lts)|
| OpenJDK (Temurin) Current | Windows | [![Build (OpenJDK (Temurin) Current, Windows)](https://img.shields.io/github/actions/workflow/status/io7m-com/streamtime/main.windows.temurin.current.yml)](https://www.github.com/io7m-com/streamtime/actions?query=workflow%3Amain.windows.temurin.current)|
| OpenJDK (Temurin) LTS | Windows | [![Build (OpenJDK (Temurin) LTS, Windows)](https://img.shields.io/github/actions/workflow/status/io7m-com/streamtime/main.windows.temurin.lts.yml)](https://www.github.com/io7m-com/streamtime/actions?query=workflow%3Amain.windows.temurin.lts)|

## streamtime

The `streamtime` package provides a simple extension to Java I/O streams that
can track transfer rates and provide statistics.

## Features

* Input and output stream implementations that track and regularly broadcast
  transfer statistics.
* High coverage test suite.
* [OSGi-ready](https://www.osgi.org/).
* [JPMS-ready](https://en.wikipedia.org/wiki/Java_Platform_Module_System).
* ISC license.

## Usage

Create a `STTimedInputStream` from an existing `InputStream`, and provide it
with a `Consumer<STTransferStatistics>` function that receives transfer updates:

```
InputStream is;
Consumer<STTransferStatistics> f;

try (var input = new STTimedInputStream(f, is)) {
  input.transferTo(...);
}
```

The `f` function will be called at a rate of roughly once per second, with
a new value of type `STTransferStatistics` describing the expected number of
octets, the current number of octets, and the current number of octets received
per second.

The `STTimedOutputStream` class works similarly, but for `OutputStream` values.

