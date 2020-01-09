# iron/go:dev is the alpine image with the go tools added
FROM iron/go:dev
WORKDIR /app

VOLUME [ "/log" ]

# Set an env var that matches your github repo name, replace treeder/dockergo here with your repo name
ENV SRC_DIR=.
# Add the source code:
ADD . $SRC_DIR
# Build it:
RUN go build -o edl
ENTRYPOINT ["./edl"]