FROM golang:1.8.4-jessie

# Install Skipper
RUN rm -rf ws \
&& mkdir ws \
&& cd ws \
&& pwd \
&& export GOPATH=$(pwd) \
&& export PATH=$PATH:$GOPATH/bin \
&& go get github.com/zalando/skipper/...