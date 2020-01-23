FROM alpine

MAINTAINER Sequoia Snow <sequoia@7mind.de>

WORKDIR /src/github.com/sevenmind/drone-webb

# Install necessary dependencies

RUN apk add --no-cache -U git jq curl bash

ADD webb .

# Make sure our script is executable and store it in the /usr/local/bin
# directory so its part of the $PATH regardless of WORKDIR

RUN chmod +x webb && cp webb /usr/local/bin/webb

ENTRYPOINT ["/usr/local/bin/webb"]
