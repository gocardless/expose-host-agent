# expose-host-agent

`expose-host-agent` is a small wrapper designed to be used around `docker
build` that does the necessary dance with your local SSH agent to allow the
build to pull content from private git repositories.

Docker commands that need access to private git repositories can then be
prepended with `with-host-agent`.

## Installation

```sh
brew tap gocardless/homebrew-taps
brew install expose-host-agent
```

## Usage

It runs whatever arguments you give it as a command, so you can use `docker
build` as normal.

To use `expose-host-agent`, simply wrap normal Docker commands in it like this:

```
expose-host-agent docker build -t test_build
```

Instead of your image failing to build, you should now see something like:


```
Step 16/16 : RUN with-host-agent git clone git@github.com:gocardless/must-have-private-dependency.git

---> Running in 2d630d625583

192.168.65.2    host.docker.internal

Cloning into 'must-have-private-dependency'...

Warning: Permanently added the RSA host key for IP address '140.82.118.4' to the list of known hosts.

Removing intermediate container 2d630d625583

---> 3370566db8f1

Successfully built 3370566db8f1
```

Et voilà!
