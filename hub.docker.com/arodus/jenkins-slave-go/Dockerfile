FROM arodus/docker-jenkins-slave-mono


ENV GOLANG_VERSION 1.10.4

RUN curl -o go.tgz https://dl.google.com/go/go${GOLANG_VERSION}.linux-amd64.tar.gz \
    && tar -C /usr/local -xzf go.tgz \
	&& rm go.tgz \
    && export PATH="/usr/local/go/bin:$PATH" \
    && go version

RUN apt-get update && apt-get install -y rsync make \
    && apt-get -q clean -y && rm -rf /var/lib/apt/lists/* && rm -f /var/cache/apt/*.bin

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

USER jenkins
ENV GOPATH /home/jenkins/go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

USER root

