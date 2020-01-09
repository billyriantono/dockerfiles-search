FROM golang:latest
LABEL maintainer="bat-cha <baptiste.chatrain@gmail.com>"

RUN curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh \
    && go get -u github.com/jstemmer/go-junit-report \
    && go get -u golang.org/x/lint/golint \
    && go get -u github.com/go-swagger/go-swagger/cmd/swagger \
    && curl -L https://codeclimate.com/downloads/test-reporter/test-reporter-latest-linux-amd64 > /bin/cc-test-reporter \
    && chmod +x /bin/cc-test-reporter
