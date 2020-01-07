FROM alpine:3.7

# BASH ----------------
RUN apk update && apk upgrade
RUN apk add --no-cache bash
COPY bashrc /root/.bashrc

ENTRYPOINT ["/bin/bash"]
