FROM ubuntu

RUN apt-get update
RUN apt-get install -y unzip

ADD http://cryptoescudo.pt/download/01030000/linux/cryptoescudo-1.3.0.0-linux.zip cryptoescudo.zip
RUN unzip cryptoescudo.zip

WORKDIR cryptoescudo-1.3.0.0-linux/64
COPY setup.sh .

RUN chmod 700 -R ./

RUN mkdir "/root/.cryptoescudo"
VOLUME ["/root/.cryptoescudo"]

CMD ["./cryptoescudod", "-printtoconsole", "-daemon"]
