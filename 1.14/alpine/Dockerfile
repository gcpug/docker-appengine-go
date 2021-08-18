FROM google/cloud-sdk:alpine
LABEL maintainer "GCPUG <https://gcpug.jp/>"

ENV GOPATH=/go \
	PATH=/go/bin:/usr/local/go/bin:/google-cloud-sdk/bin:/google-cloud-sdk/platform/google_appengine:$PATH

ARG GOLANG_VERSION=1.14.3
ARG GOLANG_DOWNLOAD_SHA256=1c39eac4ae95781b066c144c58e45d6859652247f7515f0d2cba7be7d57d2226

RUN apk add --no-cache \
        gcc \
        libc-dev \
        make \
        unzip && \
    \
    gcloud components install \
		app-engine-go \
		beta && \
    chmod +x /google-cloud-sdk/platform/google_appengine/*.py && \
    \
    curl -o go.tgz -sSL "https://golang.org/dl/go${GOLANG_VERSION}.linux-amd64.tar.gz" && \
    echo "${GOLANG_DOWNLOAD_SHA256} *go.tgz" | sha256sum -c - && \
    tar -C /usr/local -xzf go.tgz && \
    rm go.tgz

VOLUME ["/root/.config"]
