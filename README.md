# dotnet-vsdbg

## Prerequisites

ubuntu:22.04
apt update && apt install curl
apt install libicu-dev

install kubernetes extension in VS Code

## Setup

curl -sSL https://aka.ms/getvsdbgsh | bash /dev/stdin -v latest -l ~/vsdbg

cp -r ~/vsdbg /proc/<pid>/root/vsdbg

## VSCode

launch.json

{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Kubernetes: Attach to Pod (test)",
            "type": "coreclr",                     // or "node", "python", etc. depending on your app
            "request": "attach",
            "processId": "1",                // or whatever process to attach to
            "pipeTransport": {
                "pipeProgram": "kubectl",
                "pipeArgs": ["exec", "-i", "<pod name>", "-c", "<container name>", "-n", "<namespace>", "--"],
                "debuggerPath": "/vsdbg/vsdbg",
                "quoteArgs": false,
            }
        }
    }
}
