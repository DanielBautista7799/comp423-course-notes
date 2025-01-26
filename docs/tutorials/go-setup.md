# Setting up a dev container for GO

* Primary author: [Daniel Islas](https://github.com/DanielBautista7799)
* Reviewer: [Emily Chen](https://github.com/emsesc)

This tutorial is a walk-through on how you go through setting up a Go development environment using Docker dev containers in VS code. By the end of this guide, you’ll have a fully functional environment to write, compile, and run a “Hello COMP423” program in Go without having to install Go on your local machine.


## 1. Prerequisites
### **Host Machine Setup Only**

- Install [Docker](https://docs.docker.com/engine/install/) (for containers)
- Install [Visual Studio Code](https://code.visualstudio.com/download) (editing and Dev containers)
- Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) (version control)

!!! Note
    **Do not install GO directly on host machine.** Host machine should only have Docker, VS Code and Git downloaded.
    We are going to use a Docker dev container through VS code dev containers

## 2. Step-by-step overview for instructions on a new Dev Container project for GO

We will:

1. Create a blank folder (Section 3)
2. Initialize Git in that folder (Section 3)
3. Provide a Dev Container configuration (Section 4)
4. Write and run a simple “Hello COMP423” program (Section 5)

**This overview helps us see what we are going to do before we go in depth into each step.**

## 3. Start from a Blank Directory and Git Initialize

### **Create a blank folder for your new project:**

### *3.1* Create new folder (ex: 'my-go-docs'):

```bash
mkdir my-go-docs
cd my-go-docs
```

### *3.2* Initialize Git in the folder
```bash 
git init 
```

## 4. Dev Container Configuration File 
### **Create a Dev container and configure it for your new project:**

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
### What does the Dev container do?
- "name": Sets the container name in VS Code.
- "image": Uses Microsoft's prebuilt Go development Docker image.
- "features": Adds tools/configurations to the container. Left empty in this tutorial but can include utilities like Docker CLI.
- "customizations": Installs the Go VS Code extension (golang.go) for better support with IntelliSense, formatting, and debugging.

!!! Note 
    We install the Go VS Code extension: "golang.go".
    By using docker image you avoid installing it on your host.
    Do not install Go locally on your machine. We rely on the Docker dev container.

## 5. Steps to Create a New Project, Write a Basic "Hello COMP423" Program, Compile, and Run
### **Setting up Dev container to write new program** 
*5.1* Open VS Code and Reopen the folder in Dev container (VS code will detect the `.devcontainer/devcontainer.json`)

!!! tip
    To reopen the folder in dev container in VS code input 'Shift + CTRL/COMMAND + P' to open the command pallette and select to Reopen in Dev Container

*5.2*: Verify Your Go Installation
```bash
go version
```
This should return something like:
```bash
go version go1.20 linux/amd64
```
!!! Note 
    This confirms Go is installed inside the Docker container and not on your host machine.


### **Basic Program for Go**

*5.3* Inside the Dev container create a file named `main.go` in this file input code for Hello COMP423
```go
package main

import "fmt"

func main() {
    fmt.Println("Hello COMP423")
}
```
*5.4* Initialize Go modules: Create a `go.mod` file
```bash
go mod init example.com/my-go-docs
```
### **Execution**
*5.5* Run the program directly 
```bash 
go run main.go
```
This should output
```bash 
Hello COMP423
```
*5.6* Build an executable 
```bash 
go build main.go
```
This creates the file `main` which can then be run with:
```bash 
./main
```
### **Final Output**

`Hello COMP423`

!!! info 
    - `go run` is a more simple way to compile and execute at once.
    - `go build` creates a separate file that you can run as many times without needing to recompile it.



