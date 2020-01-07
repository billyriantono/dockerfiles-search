FROM gcr.io/google_containers/ubuntu-slim:0.14

RUN apt-get update -y && apt-get install wget lbzip2 bzip2 libpcsclite1 curl -y

# RUN wget https://github.com/monero-project/monero/releases/download/v0.12.2.0/monero-linux-x64-v0.12.2.0.tar.bz2

RUN wget https://downloads.getmonero.org/cli/monero-linux-x64-v0.12.2.0.tar.bz2

ADD check.sh ./

RUN chmod +x check.sh

## Running check.sh will ensure that the docker image will only produce an image if the checksum passes

RUN ./check.sh

RUN tar jvxf monero-linux-x64-v0.12.2.0.tar.bz2

ENTRYPOINT ["./monero-v0.12.2.0/monerod"]
