FROM ubuntu:16.04

WORKDIR /usr/src/app

RUN apt-get update --fix-missing
RUN apt-get install -qy python3
RUN apt-get install -y python3-pip
RUN apt-get install -y libssl-dev --fix-missing

COPY ./requirements.txt ./

RUN pip3 install --no-cache-dir -r requirements.txt

COPY . .
WORKDIR ./scripts/SymbolPriceScraper/

CMD [ "python3", "." ]


