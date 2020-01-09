# VERSION: 0.0.4
FROM golang

# enable go modules
ENV GO111MODULE=on

# set env vars for the config and download folders
ENV DOWNLOAD_PATH="/downloads"
ENV CONFIG_PATH="/config"

RUN git clone --depth 1 https://github.com/tjsoler/REM -b develop /app

WORKDIR /app


RUN go build -o main .

# set mountpoints for the host to store the config and downloads.
VOLUME [ "/downloads", "/config" ]

ENTRYPOINT ["/app/main"]
