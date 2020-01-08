FROM alpine:3.1
RUN apk update && apk add openssh-client bash
RUN addgroup -g 1000 build && adduser -u 1000 -G build -D -g "" build && \
    mkdir -p /home/build/.ssh && \
    echo -e "Host *\n   StrictHostKeyChecking no" > /home/build/.ssh/config && \
    chown -R build /home/build/.ssh