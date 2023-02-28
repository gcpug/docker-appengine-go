FROM gcr.io/google.com/cloudsdktool/cloud-sdk:alpine
LABEL maintainer "GCPUG <https://gcpug.jp/>"

ENV GOPATH=/go \
	PATH=/go/bin:/usr/local/go/bin:/google-cloud-sdk/bin:/google-cloud-sdk/platform/google_appengine:$PATH

ARG GOLANG_VERSION=1.18.10
ARG GOLANG_DOWNLOAD_SHA256=5e05400e4c79ef5394424c0eff5b9141cb782da25f64f79d54c98af0a37f8d49

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
