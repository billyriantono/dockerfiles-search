FROM alpine:3.5

#
# INSTALL BASE PACKAGES
#
RUN apk add --no-cache \
            bash \
            wget \
            curl \
            vim \
            grep \
            sed

#
# PREPARE USER MODE
#
RUN addgroup -g 10777 worker && \
    adduser -D -G worker -u 10777 worker && \
    mkdir -p /app/ && chown -R worker:worker /app/

#
# VOLUMES AND EXPOSE
#
WORKDIR "/app/"
VOLUME ["/app"]
EXPOSE 9999

#
# RUN IN USER MODE
#
USER worker
CMD ["echo", "itse me mario"]
