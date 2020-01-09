FROM alpine:3.10 AS download
RUN apk add curl
RUN curl -o /usr/local/bin/slivar -L https://github.com/brentp/slivar/releases/download/v0.1.6/slivar
RUN chmod +x /usr/local/bin/slivar

FROM alpine:3.10
RUN apk add --no-cache bash
COPY --from=download /usr/local/bin/slivar /usr/local/bin/slivar
