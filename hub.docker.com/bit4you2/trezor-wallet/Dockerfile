FROM python:alpine

RUN apk add --no-cache curl zip

WORKDIR /app

RUN curl -O -L https://wallet.trezor.io/data/mytrezor-archive.tgz
RUN echo "6ff110704fe7e7a9535a413700698228  mytrezor-archive.tgz" > mytrezor-archive.md5
RUN md5sum -c mytrezor-archive.md5

RUN tar zxvf mytrezor-archive.tgz

WORKDIR /app/mytrezor

# Run http server on port 8080
EXPOSE  8080
ENTRYPOINT ["python3", "-m", "http.server", "8080"]
