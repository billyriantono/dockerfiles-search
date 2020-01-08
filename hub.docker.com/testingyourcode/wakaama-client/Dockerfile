FROM alpine:latest

LABEL  maintainer "testingyourcode <testing.your.code@gmail.com>"

RUN apk add --no-cache cmake g++ git autoconf automake libtool make 
RUN git clone https://github.com/eclipse/wakaama.git \
        && mkdir build && cd build && cmake ../wakaama/examples/client && make


FROM alpine:latest  
#RUN apk add --no-cache ca-certificates
WORKDIR /root/
COPY --from=0 /build/lwm2mclient .

CMD ["/root/lwm2mclient","-h 127.0.0.1","-4"]
