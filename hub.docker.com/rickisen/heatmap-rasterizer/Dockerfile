FROM debian:buster

RUN printf "deb http://deb.debian.org/debian buster-backports main" >> /etc/apt/sources.list

RUN apt-get update -qq -y && \
    apt-get install -qq -y xvfb golang git && \
    apt-get -t buster-backports install -y qgis python3-qgis

VOLUME "/cache"
ENV CACHE "/cache"

EXPOSE 8000

ENV PYTHONPATH="/usr/lib/python3/dist-packages/"
ENV RASTERIZER /rasterizer
RUN mkdir $RASTERIZER
COPY ./rasterizer/ $RASTERIZER

ENV DISPLAY ":99"
ENV APP /go/src/heatmap-rasterizer
ENV GOPATH /go

WORKDIR $APP

COPY ./src/heatmap-rasterizer/ $APP

RUN go get "github.com/gorilla/mux"
RUN go get "golang.org/x/sys/unix"
RUN go install .

COPY start-prod.sh .
CMD "./start-prod.sh"
