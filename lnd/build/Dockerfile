FROM golang:1.19.2-alpine as builder
ENV GODEBUG netdns=cgo

# Install dependencies.
RUN apk add --no-cache --update alpine-sdk \
    git \
    wget \
    make

# Copy in the local repository to build from.
RUN wget https://github.com/lightningnetwork/lnd/releases/download/v0.15.5-beta/lnd-linux-amd64-v0.15.5-beta.tar.gz
RUN tar -xzf lnd-linux-arm64-v0.15.5-beta.tar.gz
RUN sudo install -m 0755 -o root -g root -t /usr/local/bin lnd-linux-arm64-v0.15.5-beta/*

# Add bash.
RUN apk add --no-cache \
    bash
    
# Copy the entrypoint script.
COPY "./start-lnd.sh" .
RUN chmod +x start-lnd.sh
