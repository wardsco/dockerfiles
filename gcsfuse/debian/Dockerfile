FROM        golang:1.10.0-stretch as builder

RUN         apt-get update && apt-get install -y \
                git && \
            go get -u github.com/googlecloudplatform/gcsfuse && \
            mkdir -p /rootfs/usr/local/bin/ && \
            mv $GOPATH/bin/gcsfuse /usr/local/bin/gcsfuse && \
            apt-get clean -y && \
            rm -rf /var/lib/apt/lists/*

###

FROM        debian:stretch-slim

# RUN         apt-get update && apt-get install -y \
#               fuse \
#               ca-certificates

COPY        --from=builder /usr/local/bin/gcsfuse /usr/local/bin/gcsfuse

ENTRYPOINT ["gcsfuse"]
CMD        ["--help"]
