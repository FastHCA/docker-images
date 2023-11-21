# Build the application from source
FROM golang:1.19-alpine

ARG BADGERLIT_VERSION="0.3.3"
ARG BADGERLIT_IMAGE_REPO="https://github.com/FastHCA/BadgerLit/archive/refs/tags/v${BADGERLIT_VERSION}.tar.gz"


ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && \
	chmod -R 777 "$GOPATH" && \
	apk add --no-cache gcc musl-dev curl && \
	apk add git && \
	apk update && \
	apk upgrade

# download & docker build
RUN cd /opt \
    && curl -fSL ${BADGERLIT_IMAGE_REPO} -o badgerlit.tar.gz \
    && tar xzf badgerlit.tar.gz \
    && cd /opt/BadgerLit-${BADGERLIT_VERSION} \
    && go mod tidy \
    && go build -tags musl -o badgerlit \
    && cp ./badgerlit /badgerlit

WORKDIR /

CMD ./badgerlit

