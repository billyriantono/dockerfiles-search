FROM golang:latest
RUN go get github.com/yudai/gotty

FROM ubuntu:latest

WORKDIR /root
EXPOSE 8080
USER root

COPY --from=0 /go/bin/gotty /bin/gotty

RUN apt update && \
    apt install -y --no-install-recommends \
      dstat \
      nmap \
      netcat \
      wget \
      iftop \
      dnsutils \
      net-tools && \
    rm -rf /var/lib/apt/lists/*
    
CMD ["/bin/gotty", "-w", "/bin/bash"]

