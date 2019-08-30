Go Modules
==========
This file joins a collection of simple explanations about *Go Modules*. Nothing
here it's a professional thoughts. I'm a newbie, so be careful when trying
anything decribed here.

## Creating a new project
Go modules have two different ways to create new projects with support to
`go.mod`. The first common way it's just pass a `module-name` as parameter to
`go mod init` command. The second and most interesting way it's using *Version
Control System* (VCS). Using VCS `go mod` will detect the module path from
upstream url.

```bash
## Add 'go.mod' support to a repository:
$ mkdir -p myproject && cd myproject
$ git init
$ git remote add origin https://github.com/user/myproject
$ go mod init
go: creating new go.mod: module github.com/user/myproject

## The content of 'go.mod' is
$ cat go.mod
module github.com/user/myproject
go 1.12

## Initialize a new local project:
$ mkdir -p myproject && cd myproject
$ go mod init myproject

## The content of 'go.mod' is
$ cat go.mod
module myproject
go 1.12

## The project tree will be something like:
myproject
├── package
│   ├── pack_test.go
│   └── pack.go
├── main.go
└── go.mod
```

## Understanding `GO111MODULE` variable
The `GO111MODULE` variable affects some behaviors for workspaces on `$GOPATH`.
This affects only when inside or outside the `src` directory under
`$GOPATH` workspaces.
> Create a new, empty directory somewhere outside `$GOPATH/src` - [Using Go Modules][]

### `GO111MODULE=auto`
This is the default value of `GO111MODULE` variable. That means the
module-aware mode is active. So, in this case it's necessary to create a new
project outside `$GOPATH` workspaces.

### `GO111MODULE=on`
Thats makes `go mod` capable to create a `go.mod` file and then create a new
project inside `$GOPATH` workspaces. Note if set `GO111MODULE=on` in a shell 
init script, that would break all the projects that don't use go modules. 

### Examples
```bash
## When GO111MODULE is 'auto', if you inside 'src' directory under '$GOPATH'
## you will see a warning and the action will be aborted.
$ go mod init
go: modules disabled inside GOPATH/src by GO111MODULE=auto; see 'go help modules'

## To void breaking up another projects without export GO111MODULE with 'on' 
## value, just put 'GO111MODULE=on' before 'go mod init'. That will be enough.
## But I'm not sure yet if this is a better way to do that. Until now nothing
## bad happens to me.
$ GO111MODULE=on go mod init
go: creating new go.mod: module path-to/myproject
```

## References
- [Using Go Modules][]
- [Go Modules Wiki](https://github.com/golang/go/wiki/Modules)
- [How do I configure golang to recognize 'mod' packages?](https://stackoverflow.com/questions/51910862/how-do-i-configure-goland-to-recognize-mod-packages)

[Using Go Modules]: https://blog.golang.org/using-go-modules
