FROM google/golang
MAINTAINER acconsta

EXPOSE 3000

# Install node and npm
RUN curl -SL https://nodejs.org/dist/v0.12.6/node-v0.12.6-linux-x64.tar.gz \
    | tar --strip-components=1 -xzC /usr/local

# Download and build grafana
RUN go get github.com/grafana/grafana
RUN cd $GOPATH/src/github.com/grafana/grafana && \
    go run build.go setup && \
    godep restore && \
    go build . && \
    npm install && \
    npm install -g grunt-cli && \
    grunt

CMD grafana -homepath="/gopath/src/github.com/grafana/grafana"
