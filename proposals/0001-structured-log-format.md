# Format log messages in a structured way

* Proposal: [SWIFTLOGGING-0001](https://github.com/akolov/swift-logging/blob/master/proposals/0001-structured-log-format.md)
* Author(s): [Alexander Kolov](https://github.com/akolov), [Alexander Saltanov](https://github.com/sashka)
* Status: **Awaiting Review**

## Introduction

Logger should be able to write messages in arbitrary and structured way in addition to plain text.
Format is configurable, good default candidate is JSON. Other options could include XML, Protocol Buffers, etc.

## Motivation

Human is not the only consumer for log messages and flattening complex structures into plain string makes logs very hard to read and process.
Structured logs will allow machine parsing and simple unified format for distributed log consumers.

## Proposed design

Default call to JSON-backed logger `logger.info("text")` would record in the following format:

```json
  {"timestamp": "2015-12-04T10:13:43+00:00", "level": "info", "event": "text"}
```

Call with a dictionary
```swift
logger.warn([
  "numeric": 1,
  "string": "arbitrary string",
  "object": customStringConvertibleObject,
  "dict": ["dict value": "something"]
])
```

produces:

```json
  {"timestamp": "2015-12-04T10:25:48+00:00", "level": "warn", "numeric": 1, "string": "arbitrary string", "object": "object's string representation", "dict": {"dict value": "something"}}
```

Plain text formatter can be build over the structured formatter by simple flattening:

```swift
logger.warn(["numeric": 1, "string": "arbitrary string", "object": customStringConvertibleObject], "dict": {"dict value": "something"})
```

produces (note that keys are sorted):

```
2015-12-04T10:25:48+00:00 WARN string="arbitrary string" "dict"="{\"dict value\": \"something\"}" "numeric"=1 "object"="object's string representation"
```

or when generating Apache-style logs we could collapse keys completely and use custom format templates:
```
"%(timestamp) %(level) %(string) %(dict) %(object)" -- %(numeric)"
```

resulting in

```
2015-12-04T10:25:48+00:00 WARN "arbitrary string" "{\"dict value\": \"something\"}" "object's string representation" -- 1
```
