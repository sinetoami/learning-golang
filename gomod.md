Go Modules
==========

## Create a project

To create a new project, simply do this:
```bash
$ go mod init
```
This command will create a `go.mod` file inside the project with the current 
path to it.

To add `go mod` support to an existing new project
```bash
$ go mod init module-name
```

The project tree will be something like:
```
myproject
├── package
│   ├── pack_test.go
│   └── pack.go
├── main.go
└── go.mod
```

## Understanding `GO111MODULES` variable
### `GO111MODULES=auto` [default]
The default value of `GO11MODULES` variable is `auto`. That means the 
module-aware mode is active. So, in this case it's necessary to create a new 
project outside `$GOPATH`.

### `GO111MODULES=on`
Thats makes `go mod` capable to create a `go.mod` file and then create a new 
project inside `$GOPATH`. Note that if set `GO111MODULES=on` in a shell init 
script, that would break all the projects that don't use go modules. To avoid
break another project, simply do this:
```bash
GO111MODULES=on go mod init
```
That will be enough.

## References
[How do I configure golang to recognize 'mod' packages?](https://stackoverflow.com/questions/51910862/how-do-i-configure-goland-to-recognize-mod-packages)
