FROM google/cloud-sdk:alpine
LABEL maintainer "GCPUG <https://gcpug.jp/>"

ENV GOPATH=/go \
	PATH=/go/bin:/usr/local/go/bin:/google-cloud-sdk/bin:/google-cloud-sdk/platform/google_appengine:$PATH

ARG GOLANG_VERSION=1.15.14
ARG GOLANG_DOWNLOAD_SHA256=6f5410c113b803f437d7a1ee6f8f124100e536cc7361920f7e640fedf7add72d

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
