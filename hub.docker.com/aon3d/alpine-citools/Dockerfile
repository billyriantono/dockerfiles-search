FROM alpine:3.10

RUN apk update && apk add \
        curl \
        openssh \
        git \
        make \
        python3 \
        gcc-avr \
        avr-libc \
        hugo

RUN git clone https://github.com/arduino/ArduinoCore-avr.git && \
        mkdir -p /usr/share/arduino/hardware/arduino && \
        mv  ArduinoCore-avr /usr/share/arduino/hardware/arduino/avr
