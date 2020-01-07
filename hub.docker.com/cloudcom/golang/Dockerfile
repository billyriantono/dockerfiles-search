FROM		golang:1.5
ENV		GOBIN $GOPATH/bin
RUN		go get github.com/tools/godep
RUN		go get github.com/CloudCom/goose/cmd/goose

EXPOSE		8080

ADD		entrypoint.sh	/entrypoint.sh
ENTRYPOINT	["/entrypoint.sh"]
