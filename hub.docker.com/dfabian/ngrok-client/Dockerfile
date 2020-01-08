FROM golang

#WORKDIR /usr/src/
RUN git clone https://github.com/Aspir-ina/ngrok.git /usr/src/ngrok
WORKDIR /usr/src/ngrok

RUN make release-client

ENTRYPOINT ["bin/ngrok"]
CMD ["help"]
