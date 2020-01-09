FROM golang:1.10.3-alpine3.8
RUN apk add \
    g++ make wget qt5-qtbase-dev libmediainfo-dev p7zip wget git

RUN cd /tmp \
 && wget https://github.com/QNapi/qnapi/releases/download/0.2.3/qnapi-0.2.3.tar.gz \
 && tar xf qnapi-0.2.3.tar.gz \
 && cd qnapi-0.2.3 \
 && /usr/lib/qt5/bin/qmake \
 && make \
 && make install \
 && cd / \
 && rm -fr /tmp/qnapi*

RUN go get -u github.com/cespare/reflex \
 && cd /go/src/github.com/cespare/reflex \
 && go install ./... \
 && go build

ENV MOVIE_FORMAT_REGEX "(\.avi|\.mov|\.mp4|\.mkv)$"

RUN pwd && ls -lah /go/src/github.com/cespare/reflex
CMD /go/src/github.com/cespare/reflex/reflex --only-files=true -e -v -r ${MOVIE_FORMAT_REGEX} -- sh -c 'qnapi -c "{}"'
