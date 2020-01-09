FROM circleci/golang:1.11

# Install tools required for the project
RUN go get -u golang.org/x/lint/golint
RUN curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh

ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/go/src/github.com/iotexproject/iotex-wallet/vendor/github.com/iotexproject/iotex-core/crypto/lib
