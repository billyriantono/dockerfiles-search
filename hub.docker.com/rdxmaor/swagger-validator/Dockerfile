FROM golang:1.12 as build

WORKDIR /build
COPY . .
RUN go build -o ./bin/swaggerValidator ./src/cmd/main.go

FROM golang:1.12 as final

ENV SWAGGER_FILE="/data/swagger.yaml"
ENV I18N_FOLDER="/data/i18n"

VOLUME [ "/data", "/data/i18n" ]

WORKDIR /app
COPY --from=build /build/bin/ .

CMD ./swaggerValidator --swagger ${SWAGGER_FILE} --i18n ${I18N_FOLDER}

