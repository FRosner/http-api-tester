# HTTP API Tester

[![Build Status](https://travis-ci.org/FRosner/http-api-tester.svg?branch=master)](https://travis-ci.org/FRosner/http-api-tester)

## Description

This is a framework for testing HTTP APIs. It let's you define your test suites and test cases in form of a simple folder structure.

## Usage

### Example

The HTTP API Tester project comes with an example test suite.
If you want the tests to pass, you need to serve the directory through an HTTP server.
Otherwise you can skip this step and see what failing tests look like.

```sh
# Clone the repo
git clone git@github.com:FRosner/http-api-tester.git
cd http-api-tester.git

# Start an HTTP server inside the git repo folder
# This requires http-server to be installed (npm install http-server -g)
# You can skip it if you want (but the tests will fail)
http-server&

# Test it
./http-api-tester example-suite

# Shut down http-server again: kill %$(jobs | grep http-server | grep -Po '\d+')
```

### Writing Tests

HTTP API Tester uses a simple directory structure to define tests.
When invoked, you specify the suite to run.
A test suite consist of one or multiple test cases.
Each test case corresponds to one HTTP request being sent.
The test case can be configured using the following parameters.
Parameters printed in _italic_ are mandatory.

- _Test case name (directory name)_
  - HTTP method (defaults to `GET`)
  - URL (defaults to `localhost:80`)
  - Request data
  - Before script
  - After script
  - Expectations
    - HTTP status
    - Response data
- Before all script
- After all script

The example suite has the following directory structure:

```
example-suite
├── correct-json-content
│   ├── expected
│   │   ├── http-status
│   │   ├── response-data
│   ├── method
│   ├── request-data
│   └── url
├── index-reachable
│   ├── before
│   ├── after
│   ├── expected
│   │   └── http-status
│   ├── method
│   ├── request-data
│   └── url
├── before-all
└── after-all
```

### Test Results

Each test run is persisted in a subfolder called `run-%Y-%m-%d-%k-%M-%S`.
It allows you to debug or save your test results for later.

```
test-suite/test-case
├── run-2016-07-15-17-03-12
│   └── ...
└── run-2016-07-16-15-00-35
    └── ...
```

If you execute a lot of tests, the results will pile up. In order to only save the latest test result, you can use the `-c` or `--clean` argument.

```
./http-api-tester -c example-suite
```

## Installation

Make sure to have your test suites ready in your project directory and the requirements set up. To run the tool, just execute:

```
bash <(curl -s https://raw.githubusercontent.com/FRosner/http-api-tester/master/http-api-tester) example-suite
```

## Requirements
- curl 7.43.0
- jq-1.5 (for JSON payload)
- cmp (GNU diffutils) 2.8.1
