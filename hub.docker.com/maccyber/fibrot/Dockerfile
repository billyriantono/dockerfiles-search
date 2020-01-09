FROM alpine
RUN apk add bash bc
RUN mkdir /src
WORKDIR /src
RUN wget https://raw.githubusercontent.com/keithieopia/fibonacci-caesar-cipher/master/fibrot
RUN chmod +x /src/fibrot
RUN mv /src/fibrot /bin
CMD fibrot
