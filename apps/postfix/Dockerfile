FROM alpine:3.16

RUN apk update && \
    apk add postfix && \
    rm -rf /var/cache/apk/*

EXPOSE 25/tcp
EXPOSE 465/tcp
EXPOSE 587/tcp

# You might need more or less map operations before startup
CMD /usr/sbin/postfix start-fg