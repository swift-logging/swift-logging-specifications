# Logger API

* Proposal: [SWIFTLOG-0003](https://github.com/akolov/swift-logging/blob/master/proposals/0003-logger-api.md)
* Author(s): [Alexander Kolov](https://github.com/akolov)
* Status: **Draft**

## Introduction

This is a public facing interface which is used by customers to configure logging facility and actually log events.

## Design principles

We want this API to be simple but flexible enough to cover all viable use-cases and minimize need of subclassing.
It's desired that we have some degree of similarity with [existing solutions](https://github.com/akolov/swift-logging/blob/master/proposals/0000-reference-projects.md) to make it easy to use for developers with all levels of proficiency in Swift.

## Proposed design

### Logger

Instances of the Logger class represent a single logging channel. Channels can represent different areas of application and it's up to the developer to define their scope. Logging channel is represented by a unique identifier.

_Can channels be nested?_

Base method to send message to logger:

```swift
func log(level level: Level, message: String, dictionary: Dictionary<String: AnyObject>?, file: String = __FILE__, function: String = __FUNCTION__, line: Int = __LINE__, column: Int = __COLUMN__) -> Void
```

### Log levels

Following log levels are proposed:

* emergency
* alert
* critical
* error
* warning
* info
* debug

_Do we need emergency and alert, can we merge them into critical?_

### Handlers

Handler instances dispatch logging events to specific destinations. Each logger instance can be configured to use any number of handlers.
Core library should include only the abstract base handler, upon which specific implementations can be built.

### Formatters

Formatter instances are used to convert an [Event](https://github.com/akolov/swift-logging/blob/master/proposals/0002-event-interface.md) to text.
_Do we need template engine for formatters?_
