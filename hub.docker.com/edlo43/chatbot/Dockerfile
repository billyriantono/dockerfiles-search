# build stage
FROM golang:alpine AS build-env
ADD . /src
RUN cd /src && go build -o app

# final stage
FROM alpine
WORKDIR /app
COPY --from=build-env /src/app /app/
COPY --from=build-env /src/config.json /app/
COPY --from=build-env /src/ctrlweb.bash /app/
RUN touch ./test
ENTRYPOINT ./app