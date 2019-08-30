Setup Go
========
I decide to use [asdf][] as my language version manager. So, this tutorial
will explain how to install Golang from that.

## Install ASDF
1. Clone from GitHub the latest version of `asdf`
```bash
$ git clone https://github.com/asdf-vm/asdf ~/.asdf --branch v0.7.4
```

2. Add to your shell
```bash
$ echo -e '\n. $HOME/.asdf/asdf.sh' >> ~/.zshrc
$ echo -e '\n. $HOME/.asdf/completions/asdf.bash' >> ~/.zshrc
```

## Install Golang using ASDF
1. Add asdf-golang plugin to ASDF
``` bash
$ asdf plugin-add golang https://github.com/kennyp/asdf-golang
```
2. Install Golang
```bash
$ asdf install golang 1.12.9

## This command will writes the version to '$HOME/.tools-versions' file
$ asdf global golang 1.12.9
```

## `GOPATH` environment variable
As the documentation says, it's possible to list more than one directory under
the `GOPATH`. To set a list of places, the value needs to be colon-separated 
string.

> The GOPATH environment variable is used to specify directories outside of
> $GOROOT that contain the source for Go projects and their binaries. -
> [GOPATH][]

> **NOTE:** Go searches each directory listed in GOPATH to find source code, 
> **but new packages are always downloaded into the first directory in the
> list.**

When the helper said *"new packages are always downloaded"*, means that happens
when you uses `go get` command to download new packages. See `go help gopath` 
for more details.

### Setup `$GOPATH`
```bash
## Setting a single workspace
echo "export GOPATH=$HOME/workspace/go" >> ~/.zshrc
echo "export PATH=$PATH:$GOPATH" >> ~/.zshrc

## Setting multiple workspaces
echo "export GOPATH=$HOME/workspace1/go:$HOME/workspace2/go" ~/.zshrc
echo "export PATH=$PATH:${GOPATH//://bin:}/bin" ~/.zshrc
```

## References
- [GOPATH][]
- [The GOPATH environment variable](http://golang.org/doc/code.html#GOPATH)

[GOPATH]: https://github.com/golang/go/wiki/GOPATH
[asdf]: https://github.com/asdf-vm/asdf

