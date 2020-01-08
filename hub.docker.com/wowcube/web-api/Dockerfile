FROM wowcube/web-api:base

ENV SRCPATH "$GOPATH/src/github.com/wowcube/web-api"

COPY ./pkg "$SRCPATH/pkg"
COPY ./main.go "$SRCPATH/main.go"

RUN cd $SRCPATH \
    && swag init -g ./pkg/api/server.go \
    && sed -i -e 's/{{.Host}}//g' ./docs/swagger.json \
    && mv ./docs $GOPATH/docs \
    && go install -v

FROM wowcube/web-api:ubuntu

COPY --from=0 /go/bin/web-api /usr/bin/web-api
COPY --from=0 /go/docs/swagger.json /go/docs/swagger.json
COPY ./swagger-ui /go/swagger-ui
RUN date '+%Y-%m-%d %H:%M:%S' > /go/build_time

WORKDIR /go
CMD [ "web-api" ]

EXPOSE 8089
