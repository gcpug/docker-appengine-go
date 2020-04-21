FROM google/cloud-sdk:latest
LABEL maintainer "GCPUG <https://gcpug.jp/>"

ARG GOPATH=/go
ENV GOPATH=${GOPATH} \
	CLOUDSDK_PYTHON=python2 \
	PATH=/go/bin:/usr/local/go/bin:$PATH

ARG GOLANG_VERSION=1.11.13
ARG GOLANG_DOWNLOAD_SHA256=50fe8e13592f8cf22304b9c4adfc11849a2c3d281b1d7e09c924ae24874c6daa

RUN set -eux && \
	apt-get update && \
	apt-get install -yqq --no-install-suggests --no-install-recommends \
		libc6-dev \
		make \
		unzip && \
	rm -rf /var/lib/apt/lists/* && \
	\
	curl -o go.tgz -sSL "https://golang.org/dl/go${GOLANG_VERSION}.linux-amd64.tar.gz" && \
	echo "${GOLANG_DOWNLOAD_SHA256} *go.tgz" | sha256sum -c - && \
	tar -C /usr/local -xzf go.tgz && \
	rm go.tgz && \
	mkdir ${GOPATH}

VOLUME ["/root/.config"]
