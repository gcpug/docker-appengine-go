FROM google/cloud-sdk:alpine
LABEL maintainer "GCPUG <https://gcpug.jp/>"

ENV GOPATH=/go \
	PATH=/go/bin:/usr/local/go/bin:/google-cloud-sdk/bin:/google-cloud-sdk/platform/google_appengine:$PATH

ARG GOLANG_VERSION=1.13.7
ARG GOLANG_DOWNLOAD_SHA256=b3dd4bd781a0271b33168e627f7f43886b4c5d1c794a4015abf34e99c6526ca3

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
