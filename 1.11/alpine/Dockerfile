FROM google/cloud-sdk:alpine
LABEL maintainer "GCPUG <https://gcpug.jp/>"

ENV GOPATH=/go \
	PATH=/go/bin:/usr/local/go/bin:/google-cloud-sdk/bin:/google-cloud-sdk/platform/google_appengine:$PATH

ARG GOLANG_VERSION=1.11.10
ARG GOLANG_DOWNLOAD_SHA256=aefaa228b68641e266d1f23f1d95dba33f17552ba132878b65bb798ffa37e6d0

RUN apk add --no-cache \
        gcc \
        libc-dev \
        make \
        unzip && \
    \
    gcloud components install \
		app-engine-go \
		beta && \
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
