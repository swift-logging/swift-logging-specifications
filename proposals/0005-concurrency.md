# Concurrency

* Proposal: [SWIFTLOG-0005](https://github.com/akolov/swift-logging/blob/master/proposals/0005-concurrency.md)
* Author(s): [Alexander Kolov](https://github.com/akolov)
* Status: **Draft**

## Introduction

The whole logging facility must be thread-safe. We have to design our implementations considering that logger instances can be accessed from different threads as well as processes that write to the same files and streams.

## Proposed design

Logger implementation should be fast and have as little locking as possible _(even better if we can reduce them to 0)_.


Handlers should assume that they will get accessed from multiple threads and employ synchronization mechanisms. For that we might need to have some implementation already in the base Handler.
Additionally, concrete handler implementations should assume that their destinations might be accessed from different threads and processes, e.g. one log file can be written by multiple processes.
