FROM alpine as builder
ENV VERSION=1.10.1
LABEL maintainer="John Dorman <dorman@ataxia.cloud>"
RUN apk update \
  && apk add --no-cache curl \
  && curl -o /tmp/nextdns.tar.gz -L -C - "https://github.com/nextdns/nextdns/releases/download/v${VERSION}/nextdns_${VERSION}_linux_arm64.tar.gz"  \
  && mkdir /tmp/nextdns \
  && tar zxf /tmp/nextdns.tar.gz -C /tmp/nextdns

FROM arm64v8/alpine
RUN apk add --no-cache ca-certificates
COPY --from=builder /tmp/nextdns /opt/nextdns
EXPOSE 53/tcp 53/udp
ENTRYPOINT ["/opt/nextdns/nextdns","run", "-config-file", "/etc/nextdns/nextdns.conf"]
