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

## Principles

The three ways:

* Systems Thinking - Focus on the overall outcome of the entire pipeline in the value chain (value chain?)
  * Consider the impacts an improvement in once place could have on another aspect of they system, team, etc
* Amplifying Feedback Loops - creating, shortening, and amplifying feedback loops. Short effective feedback loops are best
  * A problem found earlier and eliminated earlier saves money and time, each step a problem/bug/design issue survives massively increases the costs of fixing it
* Culture of Continual Experimentation and Learning - expiremnent, take risks, sharing, etc

## CAMS Model

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

## Devops tooling

* Programmable - Tools should have an API or command line interface (or at least not require a UI), otherwise they are hard to automate.
* Verifiable - Trust but verify, tool should be able to provide feedback and metrics
* Well behaved - should be able to check configuration into source control, include tests that verify its behaviour, deployable in an automated manner