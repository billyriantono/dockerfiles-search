FROM ubuntu:14.04

MAINTAINER avadhutp

LABEL description="Run query_monitor and quit after a single run."

# Install basic dependencies
RUN \
    apt-get update && \
    apt-get install -y golang git && \
    mkdir /gocode

# Set paths
ENV GOPATH /gocode
ENV PATH /gocode/bin:$PATH

# Install query_monitor
COPY dockerfiles/springhare/conf/query_monitor.yaml /etc/query_monitor.yaml
RUN go get -u github.com/avadhutp/query_monitor
ENTRYPOINT ["query_monitor"]