# HTTP API Tester

## Description

Framework for testing HTTP APIs.

## Usage

```sh
# Start an HTTP server inside the git repo folder
# This requires http-server to be installed (npm install http-server -g)
http-server&

# Test it
./http-api-tester example

# Shut down http-server again: kill %$(jobs | grep http-server | grep -Po '\d+')
```

## Requirements

- curl 7.43.0
- jq-1.5
- cmp (GNU diffutils) 2.8.1
