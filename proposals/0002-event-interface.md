# Log event interface, mandatory and optional fields

* Proposal: [SWIFTLOG-0002](https://github.com/akolov/swift-logging/blob/master/proposals/0002-event-interface.md)
* Author(s): [Alexander Kolov](https://github.com/akolov)
* Status: **Draft**

## Introduction

Log events should conform to one standard interface with a small set of mandatory properties, while being flexible enough to store additional data.

## Motivation

Log event interface should cover all major use cases and provide a single stable interface for event consumers to work with.
We need to think about future use cases, since changing it in future will break compatibility with existing consumers.

## Proposed design

I propose that we use the following interface for the log events _(why?)_:

```swift
struct Event {
  let timestamp: NSDate
  let channel: String
  let level: Level
  let sourceFilename: String
  let sourceModule: String
  let sourceFunction: String
  let sourceLine: Int
  let threadID: Int?
  let processID: Int?
  let message: String?
  let metadata: [String: AnyObject]?
}
```
