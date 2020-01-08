FROM golang:1.5.3-wheezy

RUN apt-get install git
RUN mkdir -p /usr/home/gocode
ENV GOPATH /usr/home/gocode
RUN git clone https://github.com/zachlatta/sshtron.git /usr/home/gocode/src/github/zachlatta/sshtron
WORKDIR /usr/home/gocode/src/github/zachlatta/sshtron
RUN ssh-keygen -t rsa -f id_rsa
EXPOSE 2022 3000
RUN go get && go build
ENTRYPOINT ./sshtron




