# docker-appengine-go

Docker Image for the [Google App Engine Go environment second generation](https://cloud.google.com/appengine/docs/go/).

## Installation

```sh
docker pull gcr.io/gcpug-container/appengine-go
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
| **Base image** |[google/cloud-sdk:latest](https://hub.docker.com/r/google/cloud-sdk/) |[google/cloud-sdk:slim](https://hub.docker.com/r/google/cloud-sdk/)| [google/cloud-sdk:alpine](https://hub.docker.com/r/google/cloud-sdk/)       |


## Usage

To use this image, pull from [Container Registry](https://gcr.io/gcpug-container/appengine-go). See [Installation](#installation) section.

Verify the `go`, `gcloud` and `dev_appserver.py` commands:

```console
$ docker run --rm -it gcr.io/gcpug-container/appengine-go:latest gcloud version
Google Cloud SDK 220.0.0
alpha 2018.10.08
app-engine-go
app-engine-java 1.9.66
app-engine-python 1.9.77
app-engine-python-extras 1.9.77
beta 2018.10.08
bigtable
bq 2.0.34
cbt
cloud-datastore-emulator 2.0.2
core 2018.10.08
datalab 20180823
gsutil 4.34
kubectl 2018.10.08
pubsub-emulator 2018.10.08

$ docker run --rm -it gcr.io/gcpug-container/appengine-go:latest go version
go version go1.11.1 linux/amd64

$ docker run --rm -it gcr.io/gcpug-container/appengine-go:latest which dev_appserver.py
/usr/bin/dev_appserver.py
```

### Use on Circle CI 2.0

Create `.circleci/config.yml` to your repository.

```yaml
version: 2
jobs:
  build:
    working_directory: /go/src/github.com/YOUR/REPO
    docker:
      - image: gcr.io/gcpug-container/appengine-go
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

