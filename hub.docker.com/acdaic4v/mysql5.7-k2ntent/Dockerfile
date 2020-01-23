FROM golang:1.5

RUN mkdir -p /go/src/github.com/syncthing
WORKDIR /go/src/github.com/syncthing
RUN git clone https://github.com/syncthing/syncthing.git
WORKDIR /go/src/github.com/syncthing/syncthing
RUN go get -u github.com/golang/lint/golint
RUN go run build.go

RUN cp /go/src/github.com/syncthing/syncthing/bin/* /usr/local/bin/
WORKDIR /syncthing
#COPY config.xml /syncthing/

# IHM
EXPOSE 8384
# TCP port
EXPOSE 22000

CMD /usr/local/bin/syncthing -home="/syncthing" -gui-address="0.0.0.0:8384" -logfile="-"

