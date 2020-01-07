FROM alpine
RUN apk update
RUN apk add --no-cache lftp
RUN mkdir -p ~/.lftp/
RUN echo "set ssl:verify-certificate no" > ~/.lftp/rc
