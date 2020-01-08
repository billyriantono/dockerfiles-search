FROM golang:1.10-alpine

# installing dep for git
RUN apk add --no-cache git openssh-client curl

# install dep
COPY install.sh /
RUN /install.sh
RUN rm /install.sh

# For sonar scanner
RUN apk add --no-cache openjdk8-jre
RUN wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.2.0.1873.zip && \
	unzip sonar-scanner-cli-4.2.0.1873.zip -d /opt/ && \
	rm sonar-scanner-cli-4.2.0.1873.zip

ENV PATH="${PATH}:/opt/sonar-scanner-4.2.0.1873/bin"

# Get go-junit-report
RUN go get github.com/jstemmer/go-junit-report && go install github.com/jstemmer/go-junit-report && rm -r $GOPATH/src/github.com/jstemmer/go-junit-report

CMD sh
