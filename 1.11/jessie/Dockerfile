FROM google/cloud-sdk
LABEL maintainer "GCPUG <https://gcpug.jp/>"

ENV GOPATH=/go \
	PATH=/go/bin:/usr/local/go/bin:/google-cloud-sdk/bin:/google-cloud-sdk/platform/google_appengine:$PATH

ARG APT_MIRROR=httpredir.debian.org
ARG GOLANG_VERSION=1.11.1
ARG GOLANG_DOWNLOAD_SHA256=2871270d8ff0c8c69f161aaae42f9f28739855ff5c5204752a8d92a1c9f63993

RUN sed -ri "s/(deb|httpredir).debian.org/${APT_MIRROR}/g" /etc/apt/sources.list && \
	set -eux && \
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
	rm go.tgz

VOLUME ["/root/.config"]
