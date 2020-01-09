FROM wunderai/drone-golang-kafka:latest

ADD repositories /etc/apk/repositories
RUN apk add --no-cache vips@edgecommunity
RUN apk add --no-cache vips-dev@edgecommunity
RUN apk add --no-cache fftw-dev@edgecommunity
RUN apk add --no-cache libpng-dev@edge
