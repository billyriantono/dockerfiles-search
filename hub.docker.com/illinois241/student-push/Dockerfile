FROM alpine:3.8
RUN apk add --no-cache bash git openssh && \
    mkdir -p /root/.ssh && \
    echo $'Host *\n\tStrictHostKeyChecking no' >> /root/.ssh/config && \
    chmod 400 /root/.ssh/config
ADD askpass.sh .
ADD push.sh .
ENTRYPOINT ["/bin/bash", "push.sh"]
