FROM debian

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
    curl telnet ldnsutils dnsutils wget netcat vim

ENTRYPOINT ["/bin/bash"]
