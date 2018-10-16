# docker-appengine-go
[![Docker Build Status](https://img.shields.io/docker/build/gcpug/appengine-go.svg?style=flat-square&label=status)](https://hub.docker.com/r/gcpug/appengine-go/builds/)
[![Docker Automated build](https://img.shields.io/docker/automated/gcpug/appengine-go.svg?style=flat-square&label=build)](https://hub.docker.com/r/gcpug/appengine-go/)

Docker Image for the [Google App Engine Go environment second generation](https://cloud.google.com/appengine/docs/go/).

## Installation

```sh
docker pull gcpug/appengine-go
```

## Tags

All images installed `go` runtime, `gcloud` SDK and following components with `gcloud` way.

## 2nd generation

### Go 1.11
| Tag            | [`latest`](1.11/jessie/Dockerfile), [`1.11`](1.11/jessie/Dockerfile) | [`slim`](1.11/slim/Dockerfile), [`1.11-slim`](1.11/slim/Dockerfile) | [`alpine`](1.11/alpine/Dockerfile), [`1.11-alpine`](1.11/alpine/Dockerfile) |
|---------------:|----------------------------------------------------------------------|---------------------------------------------------------------------|-----------------------------------------------------------------------------|
|         **Go** | 1.11.1                                                               | 1.11.1                                                              | 1.11.1                                                                      |
| **Components** | appengine-go                                                         | appengine-go                                                        | appengine-go                                                                |
|                | beta                                                                 | beta                                                                | beta                                                                        |
|                | cloud-datastore-emulator                                             |                                                                     |                                                                             |
|                | emulator-reverse-proxy                                               |                                                                     |                                                                             |
|                | pubsub-emulator                                                      |                                                                     |                                                                             |
| **Base image** | [debian:jessie](https://hub.docker.com/_/debian/)                    | [debian:jessie-slim](https://hub.docker.com/_/debian/)              | [google/cloud-sdk:alpine](https://hub.docker.com/r/google/cloud-sdk/)       |


## Usage

To use this image, pull from [Docker Hub](https://hub.docker.com/r/gcpug/appengine-go/). See [Installation](#installation) section.

Verify the `go`, `gcloud` and `goapp` commands:

```console
$ docker run --rm -it gcpug/appengine-go:latest gcloud version
Google Cloud SDK 167.0.0
alpha 2017.08.11
beta 2017.08.11
bq 2.0.25
core 2017.08.11
gcloud
gsutil 4.27

$ docker run --rm -it gcpug/appengine-go:latest go version
go version go1.6.4 linux/amd64

$ docker run --rm -it gcpug/appengine-go:latest goapp version
go version 1.6.4 (appengine-1.9.57) linux/amd64
```

### Use on Circle CI 2.0

Create `.circleci/config.yml` to your repository.

```yaml
version: 2
jobs:
  build:
    working_directory: /go/src/github.com/YOUR/REPO
    docker:
      - image: gcpug/appengine-go
    steps:
      - checkout
      - run:
          command: YOUR_TEST_COMMAND
```

If you want to test the CI works, Install Circle CI 2.0 Command Line Interface:

https://circleci.com/docs/2.0/local-jobs/

Verify on local (required Docker environment on host OS):

```sh
cd /path/to/your_repository
circleci build
```

## Committers

 * Kensuke Sano ([@sonatard](https://github.com/sonatard))

