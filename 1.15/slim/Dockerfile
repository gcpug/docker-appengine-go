FROM google/cloud-sdk:slim
LABEL maintainer "GCPUG <https://gcpug.jp/>"

ARG GOPATH=/go
ENV GOPATH=${GOPATH} \
	PATH=/go/bin:/usr/local/go/bin:$PATH

ARG GOLANG_VERSION=1.15.8
ARG GOLANG_DOWNLOAD_SHA256=d3379c32a90fdf9382166f8f48034c459a8cc433730bc9476d39d9082c94583b

RUN set -eux && \
	apt-get update && \
	apt-get install -yqq --no-install-suggests --no-install-recommends \
        google-cloud-sdk-app-engine-go \
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
