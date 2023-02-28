#run git clone https://github.com/lucaslorentz/caddy-docker-proxy/ ./build first in caddy dir
FROM --platform=${BUILDPLATFORM} alpine:3.17.0 as alpine
RUN apk add -U --no-cache ca-certificates
RUN apk add nss-tools

ENV XDG_CONFIG_HOME /config
ENV XDG_DATA_HOME /data

WORKDIR /

COPY --from=alpine /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/

COPY artifacts/binaries/AMD64/caddy /bin/

ENTRYPOINT ["/bin/caddy"]

CMD ["docker-proxy"]
