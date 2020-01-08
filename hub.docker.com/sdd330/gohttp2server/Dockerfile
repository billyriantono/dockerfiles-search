FROM golang
MAINTAINER yang.leijun@gmail.com

# Install packages
RUN apt-get update && apt-get -y install openssl vim

# Install go libs
RUN go get github.com/bradfitz/http2

# Make dockerfile and README self-contained in image
ADD . /app

# Define mount point to access data on host system.
VOLUME ["/www"]

# Expose ports.
EXPOSE 443

# ENTRYPOINT
ENTRYPOINT ["go"]

# CMD
CMD ["run", "/app/src/server.go"]