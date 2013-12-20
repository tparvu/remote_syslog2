# remote_syslog2

Remote_syslog tails one or more log files and sends syslog messages to a
remote central syslog server. It generates packets itself, ignoring the system
syslog daemon, so its configuration doesn't affect system-wide logging.

Uses:

 * Collecting logs from servers & daemons which don't natively support syslog
 * When reconfiguring the system logger is less convenient than a
   purpose-built daemon (e.g., automated app deployments)
 * Aggregating files not generated by daemons (e.g., package manager logs)

This code is tested with the hosted log management service
[Papertrail](https://papertrailapp.com) and should work for transmitting to
any syslog server.

remote_syslog2 is a rewrite of the ruby
[remote_syslog](https://github.com/papertrail/remote_syslog) package. Not all
features of the ruby version are supported, and there are some backwards
incompatible changes.

# Installing

Precompiled binaries are coming soon. Until then, install using the
development instructions below.

# Usage

(todo)

# Development

remote_syslog2 is written in go, and uses [godep](https://github.com/kr/godep)
to manage dependencies. To get everything set up, install go then run:

    go get github.com/kr/godep

    # once the repo isn't private we can just run "go get" here
    mkdir -p $GOPATH/src/github.com/sevenscale
    cd $GOPATH/src/github.com/sevenscale
    git clone git@github.com:sevenscale/remote_syslog2.git
    cd remote_syslog2

To run tests:

    # run all tests
    godep go test ./...
    # run all tests except the slower syslog reconnection tests
    godep go test -short ./...

To create a compiled executable:

    godep go build -o remote_syslog2 .

To build a tarball for release:

   ./build.sh

# Logging Configuration
Levels: TRACE,DEBUG,INFO,WARNING,ERROR
Modules <root>, syslog

remote_syslog uses a hierarchical logger that allow you to control the logging level of various packages. The default configuration is <code>\<root\>=INFO</root></code>

## Examples

- Increase the verbosity of all packages

```
remote_syslog -log "<root>=DEBUG"
```


- Set the root logger to debug and the syslog package to trace

```
remote_syslog -log "<root>=DEBUG;syslog=TRACE"
```
