FROM golang:1.10.0
MAINTAINER Yasushi kobayashi <ptpadan@gmail.com>

ENV TZ=Asia/Tokyo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN go get github.com/tockins/realize && \
  go get github.com/eure/kamimai/cmd/kamimai
