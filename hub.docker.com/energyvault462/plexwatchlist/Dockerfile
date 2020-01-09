FROM golang:latest
LABEL maintainer="Brent Johnson <brentj433@gmail.com>"

WORKDIR $GOPATH/src/github.com/energyvault462/plexwatchlist

COPY . .

# Download all the dependencies
RUN go get -d -v ./...

# Install the package
RUN go install -v ./...

# This container exposes port 8080 to the outside world
EXPOSE 8080

# Run the executable
CMD ["plexwatchlist"]