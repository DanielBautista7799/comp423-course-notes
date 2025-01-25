# Setting up a dev container for GO

* Primary author: [Daniel Islas](https://github.com/DanielBautista7799)
* Reviewer: [Emily Chen](https://github.com/emsesc)

## 1. Prerequisites
**Host Machine Setup Only**

- Install Docker (for containers)
- Install Visual Studio Code (editing and Dev containers)
- Install Git (version control)

!!! Note
    **Do not install GO directly on host machine.** Host machine should only have Docker, VS code and Git downloaded.
    We are going to use a Docker dev container through VS code dev containers

## 2. Step-by-step overview for instructions on a new Dev Container project for your language

We will:

1. Create a blank folder (Step 3)
2. Initialize Git in that folder (Step 3)
3. Provide a Dev Container configuration (Step 4)
4. Write and run a simple “Hello COMP423” program (Step 5)

**This overview helps us see what we are going to do before we go indepth into each step.**

## 3. Start from a Blank Directory and Git Initialize

 **Create a blank folder for your new project:**

 *Step 1:* Create new folder (ex: 'my-go-docs'):

```bash
mkdir my-go-docs
cd my-go-docs
```

*Step 2:* Initialize Git in the folder
```bash 
git init 
```

## 4. Dev Container Configuration File 
Add a Dev container configuration by creating `.devcontainer/devcontainer.json`
```json
{
    "name": "Go Dev Container",
    "image": "mcr.microsoft.com/vscode/devcontainers/go:latest",
    "features": {},
    "customizations": {
        "vscode": {
            "extensions": [
                "golang.go"
            ]
        }
    }
}
```
!!! Note 
    We install the Go VS Code extension: "golang.go".
    By using docker image you avoid installing it on your host.
    Do not install Go locally on your machine. We rely on the Docker dev container.

## 5. Steps to Create a New Project, Write a Basic "Hello COMP423" Program, Compile, and Run
*Step 1:* Open VS Code and Reopen the folder in Dev container (VS code will detect the `.devcontainer/devcontainer.json`)

!!! Note
    To reopen the folder in dev container in VS code input 'Shift + CTRL/COMMAND + P' to open the command pallette and select to Reopen in Dev Container

*Step 1.5*: Verify Your Go Installation
```bash
go version
```
This should return something like:
```bash
go version go1.20 linux/amd64
```
!!! Note 
    This confirms Go is installed inside the Docker container and not on your host machine.



*Step 2:* Inside the Dev container create a file named `main.go` in this file input code for Hello COMP423
```go
package main

import "fmt"

func main() {
    fmt.Println("Hello COMP423")
}
```
*Step 3:* Initialize Go modules: Create a `go.mod` file
```bash
go mod init example.com/my-go-docs
```
*Step 4:* Run the program directly 
```bash 
go run main.go
```
This should output
```bash 
Hello COMP423
```
*Step 5:* Build an executable 
```bash 
go build main.go
```
This creates the file `main` which can then be run with:
```bash 
./main
```
**When ran outputs:**

`Hello COMP423`

!!! info 
    - `go run` is a more simple way to compile and execute at once.
    - `go build` creates a separate file that you can run as many times without needing to recompile it.



