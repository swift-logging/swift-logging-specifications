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
  let timestamp: NSDate # or NSTimeInterval? what kind of precision do we need?
  let channel: String
  let level: Level
  let source: (file: String, function: String, line: Int, column: Int) # Shall we make this a struct or flatten into Event?
  let process: (processID: Int, threadID: Int) # Shall we make this a struct or flatten into Event?
  let message: String?
  let metadata: [String: AnyObject]?
}
```
