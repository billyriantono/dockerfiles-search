FROM uton/golang:latest

COPY . /src
WORKDIR /src

#RUN go get -v -u github.com/labstack/echo
#RUN go get -v -u github.com/roistat/go-clickhouse
#RUN go get -v -u github.com/labstack/echo/middleware
#RUN go get -v -u github.com/olebedev/config
RUN go build -i -o ../bin/app .
RUN cp properties.yaml ../properties.yaml
RUN rm -rf properties.yaml ./*
RUN mv ../properties.yaml properties.yaml

ENTRYPOINT ../bin/app -production

EXPOSE 8081