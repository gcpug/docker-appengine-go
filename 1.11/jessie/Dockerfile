FROM debian:jessie
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
		curl \
		gcc \
		git \
		libc6-dev \
		make \
		openjdk-7-jdk \
		openssh-client \
		python-dev \
		python-pip \
		unzip && \
	rm -rf /var/lib/apt/lists/* && \
	\
	pip install -U crcmod && \
	rm -rf $HOME/.cache/pip && \
	\
	curl https://sdk.cloud.google.com | bash -s -- --disable-prompts --install-dir=/ && \
	gcloud config set core/disable_usage_reporting true && \
	gcloud config set component_manager/disable_update_check true && \
	gcloud config set metrics/environment github_docker_image && \
	\
	gcloud components install \
		app-engine-go \
		beta \
		cloud-datastore-emulator \
		emulator-reverse-proxy \
		pubsub-emulator && \
	\
	chmod +x \
		/google-cloud-sdk/platform/google_appengine/goapp \
		/google-cloud-sdk/platform/google_appengine/godoc \
		/google-cloud-sdk/platform/google_appengine/gofmt \
		/google-cloud-sdk/platform/google_appengine/appcfg.py \
		/google-cloud-sdk/platform/google_appengine/backends_conversion.py \
		/google-cloud-sdk/platform/google_appengine/bulkload_client.py \
		/google-cloud-sdk/platform/google_appengine/bulkloader.py \
		/google-cloud-sdk/platform/google_appengine/download_appstats.py \
		/google-cloud-sdk/platform/google_appengine/endpointscfg.py && \
	\
	curl -o go.tgz -sSL "https://golang.org/dl/go${GOLANG_VERSION}.linux-amd64.tar.gz" && \
	echo "${GOLANG_DOWNLOAD_SHA256} *go.tgz" | sha256sum -c - && \
	tar -C /usr/local -xzf go.tgz && \
	rm go.tgz

VOLUME ["/root/.config"]
