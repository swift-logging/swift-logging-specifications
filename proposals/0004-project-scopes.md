# Project scopes

* Proposal: [SWIFTLOG-0004](https://github.com/akolov/swift-logging/blob/master/proposals/0004-project-scopes.md)
* Author(s): [Alexander Kolov](https://github.com/akolov)
* Status: **Draft**

## Introduction

We need to define projects we need to tackle and their scopes.

## Motivation

Ideally we want swift-logging to become part of the [Foundation](https://github.com/apple/swift-corelibs-foundation), so the core library must be developed in the spirit of the Foundation and be as minimal as possible without any external dependencies.
We could also develop concrete implementations of handlers and formatters, but they would have to be installed with package manager as a separate library.
_Some basic concrete handlers and formatter could also be part of the core?_

## Proposed projects

 * logging-core
 * logging-stream-handler
 * logging-file-handler
 * logging-syslog-handler
 * logging-asl-handler
 * logging-network-handler (includes both client and server)
 * logging-mysql-handler
 * logging-postgresql-handler
 * logging-string-formatter
 * logging-json-formatter
 * logging-protobuf-formatter
