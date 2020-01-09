FROM alpine:3.5 AS builder
RUN apk update && \ 
      apk add --update alpine-sdk 
RUN mkdir /app 
WORKDIR /app 
COPY hello.c /app 
RUN mkdir bin 
RUN gcc -Wall -Werror hello.c -o bin/hello 

FROM alpine:3.5
COPY --from=builder /app/bin/hello /app/h
CMD /app/h
