FROM golang:1.6

RUN go get -u github.com/odeke-em/drive/cmd/drive \
	&& cp bin/drive /bin/ 
VOLUME /opt/drive
WORKDIR /opt/drive
ENTRYPOINT ["/bin/drive"]
