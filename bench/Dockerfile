FROM alpine

MAINTAINER matsuu@gmail.com

RUN \
  apk update && \
  apk upgrade && \
  apk add --virtual .all curl git go unzip && \
  GOPATH=/opt/go CGO_ENABLED=0 go get github.com/catatsuy/private-isu/benchmarker && \
  GOPATH=/opt/go CGO_ENABLED=0 go install github.com/catatsuy/private-isu/benchmarker && \
  ( \
    cd /opt/go/src/github.com/catatsuy/private-isu/benchmarker/userdata/ && \
    curl -sLO https://github.com/catatsuy/private-isu/releases/download/img/img.zip && \
    unzip -q img.zip && \
    rm img.zip \
  ) && \
  apk del --purge .all

ENTRYPOINT ["/opt/go/bin/benchmarker", "-u", "/opt/go/src/github.com/catatsuy/private-isu/benchmarker/userdata"]
#CMD ["-t", "http://127.0.0.1/"]
