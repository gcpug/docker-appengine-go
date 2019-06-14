FROM google/cloud-sdk:slim
LABEL maintainer "GCPUG <https://gcpug.jp/>"

ARG GOPATH=/go
ENV GOPATH=${GOPATH} \
	PATH=/go/bin:/usr/local/go/bin:$PATH

ARG GOLANG_VERSION=1.11.10
ARG GOLANG_DOWNLOAD_SHA256=aefaa228b68641e266d1f23f1d95dba33f17552ba132878b65bb798ffa37e6d0

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
