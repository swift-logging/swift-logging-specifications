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

If you'd like to participate in the Swift Standard Logging Community, we'd love to have you!

We use **[GitHub Issues](https://guides.github.com/features/issues/)** for all project planning and communication.

Contributing can take many forms:

- Making Suggestions and Pointing Out Problems
	- Reporting bugs
	- Sending feature requests
	- Pointing out typos
	- Commenting on existing issue tickets

- Improving the Documentation and Codebase
	- Fixing bugs
	- Tweaking project file settings
	- Writing unit tests
	- Submitting performance and other code improvements
	- Adding new features

Regardless of how you'd like to contribute, the first place to go is our project's Issues tab.

Please familiarize yourself with the existing issues before creating a new one, as we'd like to avoid duplicate work and administrative clutter. We won't hesitate to close duplicate or invalid issues; do not be offended.

If your intended contribution to the project isn't covered by an existing issue, please create a new issue and apply one of the following issue labels:

- **question** — If you have a question for the community or need help with something, use this label 
- **bug** — Use this label if existing functionality is not working as expected
- **improvement** — This applies to anything else: feature requests, typo fixes, documentation improvements, new feature implementations, etc.

**Note:** The team may add more labels to your issues after they've been created, but for new issues, please limit yourself to using only the labels listed above.

##### Pull Requests 

If your issue requires changes to the repository in order to be resolved—in other words, if you're contributing a change in code, documentation or project configuration—then creating the issue is just the first step.

In such cases, valid issues can only be closed once a proposed repository change has been merged in or rejected.

We use GitHub's [Pull Request](https://help.github.com/articles/using-pull-requests/) feature to handle the workflow for this: 

1. [Fork the repo](https://help.github.com/articles/fork-a-repo/) to which you'd like to submit a contribution
2. Commit changes to your fork
3. Push your changes to GitHub
4. Submit a pull request from your changes

**Important:** Unless you are a project collaborator, **we require that each pull request be associated with an open GitHub Issue**. Please note the issue number in your pull request to help us keep track of what your changes are intended to address.

#### Acknowledgements

Special thanks to [Alex Kolov](mailto:me@alexkolov.com) for setting up this repo and maintaining the Swift Standard Logging Community mailing list.
