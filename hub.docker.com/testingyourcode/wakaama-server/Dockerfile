FROM alpine:latest

LABEL  maintainer "testingyourcode <testing.your.code@gmail.com>"

RUN apk add --no-cache cmake g++ git autoconf automake libtool make 
RUN git clone https://github.com/eclipse/wakaama.git \
        && mkdir server && cd server && cmake ../wakaama/examples/server && make


FROM alpine:latest  
#RUN apk add --no-cache ca-certificates
WORKDIR /root/
COPY --from=0 /server/lwm2mserver .
EXPOSE 5683/udp 5684/udp
CMD ["/root/lwm2mserver"]
