FROM ubuntu:18.04
RUN apt-get update && apt-get install --no-install-recommends -y\
  libssl1.0.0 \
  && rm -rf /var/lib/apt/lists/*

#RUN mkdir /app \
#  && curl -L https://github.com/philippe44/AirConnect/raw/master/bin/aircast-x86-64 -o /app/aircast \
#  && chmod +x /app/aircast

ADD https://github.com/philippe44/AirConnect/raw/master/bin/aircast-x86-64 /app/aircast
RUN chmod +x /app/aircast

WORKDIR /app

CMD ["/app/aircast", "-Z", "-l", "1000:2000", "-d", "all=error", "-d", "main=info"]
