FROM ubuntu:18.04

WORKDIR /app

RUN apt-get update \
	&& apt-get install --yes apt-transport-https wget gnupg \
	&& wget -qO - https://apt.z.cash/zcash.asc | apt-key add - \
	&& echo "deb [arch=amd64] https://apt.z.cash/ jessie main" | tee /etc/apt/sources.list.d/zcash.list \
	&& apt-get update \
	&& apt-get install --yes zcash \
	&& rm -rf /var/lib/apt/lists/*

RUN zcash-fetch-params

RUN echo "addnode=mainnet.z.cash" > /app/zcash.conf

VOLUME [ "/app/data" ]

ENTRYPOINT [ "zcashd", "-conf=/app/zcash.conf", "-datadir=/app/data", "-printtoconsole" ]
