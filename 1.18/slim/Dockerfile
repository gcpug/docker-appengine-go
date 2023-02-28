FROM gcr.io/google.com/cloudsdktool/cloud-sdk:slim
LABEL maintainer "GCPUG <https://gcpug.jp/>"

ARG GOPATH=/go
ENV GOPATH=${GOPATH} \
	PATH=/go/bin:/usr/local/go/bin:$PATH

ARG GOLANG_VERSION=1.18.10
ARG GOLANG_DOWNLOAD_SHA256=5e05400e4c79ef5394424c0eff5b9141cb782da25f64f79d54c98af0a37f8d49

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
