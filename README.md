# Swift Standard Logging: Specifications

The Swift Standard Logging Community has created this repo to work towards a set of specifications for a pure Swift logging engine.

In order of priority, the goals of this project are to:

1. Define a standard Swift logging API that can run on every platform supported by Swift
2. Deliver a fully functional reference implementation of the logging API on at least one Swift platform
3. Port the logging engine to the remaining Swift platforms

### Definitions

A *logging engine* refers both to a public *logging API* and an implementation thereof.

Developers use the public API provided by a logging engine to send messages to an underlying *log facility*, which handles messages in an implementation-specific (and potentially platform-specific) way.

Examples of log facilities are:

- The system console
- A log file
- A network logging endpoint
- A platform-provided service such as the Apple System Log (ASL)

The logging engine also provides a *log facility implementation API* to provide support for sending messages to various types of log facilities. Each different type of log facility will require an implementation of this API.

### Assumptions

To reflect the fact that (1) Swift can run on multiple operating systems, and (2) logging often has a platform-specific component, we assume:

1. Our specification will declare two separate sets of APIs:
	1. A high-level logging API intended for the general public
	2. A low-level implementation API for log facility providers

2. The implementation of the high-level logging API will be pure Swift with no platform-specific dependencies

3. Implementations of low-level log facilities *should* be pure Swift but *may* have platform-specific dependencies
	- On Apple platforms, for example, the Apple System Log (ASL) is a facility a logging engine would be expected to support; however, logging code that uses ASL won't compile on other platforms because ASL is platform-specific

### The Process

The sections below outline the various phases in the process of designing and building our Swift logging engine.

#### Investigation

Before we can begin defining a Swift logging API, we should collect information on the following:

- Existing Swift logging projects
	- Evaluate API design
	- Performance considerations
		- Consider developing a suite of benchmark tests for evaluation
	- List pros & cons

- State-of-the-art of logging packages for other languages
	- How is logging most often handled in other major languages?
	- What works, and what doesn't?
	- What is applicable to Swift?

#### Requirements Drafting

Based on our research during the investigation phase, we will draft the set of requirements we wish to fulfill with our logging specification.

#### API Design

Once our requirements have been defined, we will design an API that can fulfill those requirements.

#### Reference Implementation

We will select one or more Swift platforms for building a *reference implementation*. The reference implementation is intended to serve as an example of our ideal implementation of the APIs.

##### Why not target all platforms at once?

Our ultimate goal is to ship a logging engine capable of running on every platform Swift supports.

However, that is a big job, and cross-platform Swift is bleeding-edge, as are the developer tools.

Because each platform may require customized support, our *first* priority is to create a first-class reference implementation that can serve as a model for other platforms.

Full cross-platform support is a priority, too; it will just come later.

### The Swift Standard Logging Community

We're just getting started, and we welcome your help!

#### Contributing

If you wish to be part of the discussion driving the direction of this project, please [join our mailing list](http://swiftlogging.org/mailman/listinfo/swift-logging-dev_swiftlogging.org).

If you wish to contribute via changes to this repo, please submit a pull request.

#### Acknowledgements

Special thanks to [Alex Kolov](mailto:me@alexkolov.com) for setting up this repo and maintaining the Swift Standard Logging Community mailing list.
