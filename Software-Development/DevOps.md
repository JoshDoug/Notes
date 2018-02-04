# DevOps

* [The Agile Admin](https://theagileadmin.com/what-is-devops)

The practice of operations and development engineers participating together in the entire service lifecycle, from design through the development process to production support.

DevOps involves the collaboration of everyone on the Devlopment side (programmers, QA, front-end designers) and the Operations side (Linux admins, network admins, DBAs)

Why DevOps? - According to Puppet Labs

* High-performing IT organisations deploy more frequently, fail less, and recover faster.
* Lean management and continuous delivery practices help deliver value faster.
* High performance is achievable whether your apps are greenfield, brownfield, or legacy. What?

## Basics

A (very American) breakdown of 'The Five Levels of Devops':

* Values
* Principles
* Methods
* Practices
* Tools

### Principles

The three ways:

* Systems Thinking - Focus on the overall outcome of the entire pipeline in the value chain (value chain?)
  * Consider the impacts an improvement in once place could have on another aspect of they system, team, etc
* Amplifying Feedback Loops - creating, shortening, and amplifying feedback loops. Short effective feedback loops are best
  * A problem found earlier and eliminated earlier saves money and time, each step a problem/bug/design issue survives massively increases the costs of fixing it
* Culture of Continual Experimentation and Learning - expiremnent, take risks, sharing, etc

### CAMS Model

DevOps core values:

* Culture
* Automation
* Measurement - need metrics, but need to watch the right metrics
* Sharing - openness and transparency

## Devops Methodologies

Five main Devops methodologies:

* People over Process over Tools
* Continuous Delivery
* Lean Managmenet - work in small batches, work in progress limits, feedback loops, visualisation
* Change Control - eliminate fragile artifacts, create a repeatable build process, manage dependencies, create an environment of continuous improvement
* Infrastructure as Code - Systems treated like code, checked into source control, reviewed built & tested, managed programmatically, systems should not be hand crafted

### Devops tooling

* Programmable - Tools should have an API or command line interface (or at least not require a UI), otherwise they are hard to automate.
* Verifiable - Trust but verify, tool should be able to provide feedback and metrics
* Well behaved - should be able to check configuration into source control, include tests that verify its behaviour, deployable in an automated manner

### DevOps with IT and Software Development Methodologies

* Agile - note later
* Lean - note later
* ITIL - Information Technology Infrastructure Library, a UK Gov Standard
* ITSM - Information Technology Service Management
* SDLC - System Development Lifecycle

## Infrastructure Automation - Infrastructure as Code

* Describe infrastructure in code, e.g. as a script or JSON
* Automate infrastrucutre - quicker and avoids random human mistakes, avoid UIs - CLI or REST APIs are best
  * Run it through a CI pipeline and deploy it
* Check in infrastructure configuration to source control
* This helps to ensure the dev, qa, and production environments are the same
* Testable, unit testing infrastructure
* [Infrastrctures.org](http://www.infrastructures.org/)
* Infrastructure as cattle not pets

### Configuration Management

* Provisioning - making a server ready for operation, including hardware, OS, system services, and network connectivity
* Deployment - automatically deploying and upgrading applications on a server
* Orchestration - performing coordinated operations across multiple systems
* Configuration Management - management of change control for system configuration after initial provision; maintaining and upgrading the application and application dependencies
* Imperative/procedural - commands necessary to produce a desired state are defined and executed
* Declarative/functional - a desired state is defined, relying on the tool to configure a system to match that state
* Idempotent - the ability to execute the CM procedure repeatedly, resulting in the same outcome
* Self service - the ability for an end user to initiate a process without having to go through other people

### Immutable deployment

With containers the operating system can simply be treated as another level of the application artifact. Instead of updating the operating system, simply roll out newer versions of the containers and replace the prior deployments. Thus once a container is deployed, it is considered immutable and is never directly changed/updated/reconfigured. Its state should remain consistent. This isn't always possible with datastores, although it's becoming more straightforward with NoSQL datastores.

Containers are also allowing artifacts to be managed more like code, with versioning and semantics, they can even be built with the same build tools such as Maven with a plugin and then pushed to a repository such as artifactory.

### Infrastructure Toolchain

Think Puppet, Chef, Docker Swarm, Kubernetes, Apache Mesos, and Puppet's Habitat.

## Continuous Integration & Delivery

* Continuous Integration - the practice of automatically building and unit testing the entire application frequently, ideally on every source code check in/commit
* Continuous Delivery - the additional practice of deploying every change to a production like environment, and performing automated integration and acceptance testing.
* Continuous Deployment - extends the prior two points, to where every change goes through full enough automated testing that it's deployed automatically to production. Large scale web properties such as Facebook, Etsy, and Wealthfront use continuous deployment.

Shrinking the lifecycle of updates and even of feature development improves code quality and performance. Shortlived branches and fewer of them are indicative of a higher quality project and product.

Code -> Build -> Unit Tests -> Code Validation -> Packaging -> Artifact, but every commit, not every release.

General guidelines:

* Builds should pass the coffee test - it should take less than 5 minutes.
* Commit small bits
* Don't leave the build broken, delay everything else until the build works (delay meetings etc)
* Use a trunk-based development flow - avoid long running branches (somewhat contreversial)
* Don't allow flaky test - tests that sometimes pass and sometimes fail for no apparent reason need to be fixed
* Build should return a status (pass or fail), a log (record of all tests run and the results), and an artifact which should be uploaded and tagged with a build number.

Five practices for continuous delivery:

* Only build artifacts once
* Artifacts should be immutable
  * Creates trust - all teams have confidence the artifact is the same so dev, ops, and QA all have confidence the application hasn't been altered when debugging an issue. A checksum is good here for proving this.
  * Auditability - trace specific code versions in source control to successful build artifacts to a running system
* Deployment should go to a copy of production - pre-production and production environments should be as close to identical as possible (easier in the cloud)
* Stop deploys if a previous step fails
* Deployments should be idempotent

### The role of QA

* Unit testing
* Code hygiene - best practices for the languages and frameworks being used are adhered to, use linting, code formatting, remove/replace deprecated functions
* Integration testing
* Security testing
* TDD/BDD/ATDD
* Infrastructure testing
* Performance testing

### The CI Toolchain

* Version control - Git on GitHub, GitLab, etc
* CI systems - Jenkins, Travis, CircleCI, TeamCity
* Build - Make/Rake, Maven, Gradle, Gulp, Packer
* Test - JUnit, PHPUnit, golint/gofmt, RuboCop
  * Integration & acceptance testing with Robot, Protractor, Cucumber, Selenium, Sauce Labs
* Artifact repository - Artifactory, Nexus, Docker Hub (or internal Docker registry)
* Deployment - Rundeck, Deployinator

## Reliability Engineering

Engineering doesn't end with deployment.

* MTTF - Mean Time to Failure
* MTBF - Mean Time Between Failures

Note - haven't taken notes for reliability engineering. Enterprise level deployment devops isn't relevant to me.

### Metrics and Monitoring

TKTK

### Logging

* Centralised logs.
* Only log what needs to be logged
* Only store logs as long as they might be needed
* Log all you can, but only alert what you must respond to
* Clearly define log errors
* Logs change

TKTK

### SRE Toolchain

Monitoring tools:

* graphite
* grafana
* statsd
* ganglia
* InfluxDB
* OpenTSDB
* metrics.dropwizard.io
* Pingdom
* Datadog
* Netuitive
* Ruxit
* Librato
* New Relic
* AppDynamics
* Container monitoring tools:
  * Prometheus
  * Sysdig

Log Management:

* Splunk
* Sumo Logic
* Elk stack
* Pagerduty
* VictorOps
* Flapjack.io
* Statuspage.io

TKTK

## Security & DevOps

* [Gauntlt](http://gauntlt.org/)
* Security should be brought into the fold in the same way Ops was with DevOps, instead of the chuck it over the wall mentality.

TKTK

## Resources

Books I will never read (in order of 10 to 1 for some reason):

* Visible Ops
* Continuous Delivery by Jez Humble & David Farley
* Release It!
* Effectivce DevOps
* Lean Software Development, An Agile Toolkit
* Web Operations
* The Practice of Cloud System Administration
* The DevOps Handbook
* Leading The Transformation
* The Phoenix Project - top recommendation

Twitter:

* garethr
* devopsdotcom
* ashimmy
* ernestmueller
* wickett

Newsletters:

* DevOps Weekly

Websites:

* Devops.com
* DZone & InfoQ have DevOps channels/categories
* devopscafe.org - also a podcast