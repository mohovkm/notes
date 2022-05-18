## Notes for Go newcomer (that is me right now)

#### Build go module
```bash
go build main.go
```

#### Run go module without compiling, as script (Go compiler does compile module to binary, but puts it into temporary folder, and deletes after execution)
```bash
go run main.go
```

#### Insall anything (it will be installed into $HOME/go/bin directory)
```bash
go install golang.org/x/lint/golint@latest
go install golang.org/x/tools/go/analysis/passes/shadow/cmd/shadow@latest
```

#### Linters and formatters
```bash
go fmt . # format current files
goimports -l -w . # fix imports
golint ./... # start linting whole project
go vet ./... # start linting with errors, that golint can't catch
golangci-lint run # run all needed linters at the same time. Must be installed explicitly. Configured with .golangci.yml
```

### Use different Go version
```bash
go get golang.org/dl/go.1.15.6
go1.15.6 download
go1.15.6 build
```
