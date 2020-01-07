FROM alpine:3.10.3

WORKDIR /

RUN apk update \
    # Update and updgrage alpine packages
    && apk upgrade \
    # Install required packages
    && apk --no-cache add bash ca-certificates libc6-compat tzdata 

EXPOSE 2000/udp

CMD ["bash"]