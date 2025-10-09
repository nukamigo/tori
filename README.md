# tori
Tori is a project based on Zuul (a Project gating CI system) written in Go

![Zuul components architecture](https://zuul-ci.org/docs/zuul/latest/_images/graphviz-49bbfd5e1939eebfbca92bb36b8647d309b9cd2f.png)

## Zuul Components
1. **Scheduler** - The brain of Zuul that coordinates all activities. It manages the event queue, determines which jobs to run, and communicates with source code management systems like GitHub and Gerrit. The scheduler also handles database interactions and distributes work to other components.
2. **Executor** - The component responsible for actually running jobs on nodes provided by Nodepool. Executors connect to job nodes via SSH, execute the playbooks/tests, and stream logs. They communicate with the scheduler through ZooKeeper and can emit metrics to statsd.
3. **Merger** - Handles git repository operations like cloning and merging changes. The merger prepares the code for testing by combining proposed changes with the target branch, which is especially important for project gating workflows. 
4. **Web Server** - Provides the web interface and REST API for Zuul. It connects to the database, GitHub, ZooKeeper, and executors to display build status, logs, and other information to users. 
5. **Finger Gateway** - Routes live log streams from executors to the web interface, particularly useful when executors are distributed across multiple datacenters or zones where direct connections aren't possible. 
6. **Finger Gateway** - Routes live log streams from executors to the web interface, particularly useful when executors are distributed across multiple datacenters or zones where direct connections aren't possible.
7. **Database (External Dependency)** - An external SQL database that both the scheduler and web server use to store and retrieve build history, artifacts, and other persistent data.

## Tools used for development and installed through devbox
1. Linters and Static Analysis
   - [golangci-lint](https://github.com/golangci/golangci-lint)
   - [staticcheck](https://github.com/dominikh/go-tools)
   - [errcheck](https://github.com/kisielk/errcheck)
2. Debugging
   - [Delve](https://github.com/go-delve/delve)
   - [pprof](https://pkg.go.dev/net/http/pprof)
3. Pre-Commit Hooks
   - [lefthook](https://lefthook.dev/intro.html)
