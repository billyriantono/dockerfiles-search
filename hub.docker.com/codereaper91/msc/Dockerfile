# Build image
FROM alpine:3.9 as build

## Install dependecies
RUN apk add --no-cache build-base cmake boost-dev cairo-dev

## Set environment
WORKDIR /usr/src/app
ADD . .

RUN cmake . && cpack

# Base image
FROM alpine:3.9

## Install dependecies
RUN apk add --no-cache boost boost-program_options cairo

## Add files
COPY --from=build /usr/src/app/MSC-*-Linux.sh /tmp/installer.sh

## Install file
RUN /tmp/installer.sh --prefix=/usr/local --skip-license --exclude-dir

## Entry point command
CMD [ "sh" ]
