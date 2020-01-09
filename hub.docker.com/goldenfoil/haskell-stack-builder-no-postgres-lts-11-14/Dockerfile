FROM haskell:8.2.2

WORKDIR /app
RUN mkdir donor
WORKDIR /app/donor
ADD . /app/donor

RUN stack setup
RUN stack build

WORKDIR /app
RUN rm -rf ./donor