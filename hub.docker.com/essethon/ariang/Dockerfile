FROM nginx

RUN apt-get update && apt-get install -y aria2 wget unzip && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Create conf dir and download dir
RUN mkdir /root/.aria2 && \
    mkdir /data

# AriaNg
WORKDIR /usr/share/nginx/html
RUN rm -rf /usr/share/nginx/html/*
RUN wget --quiet https://github.com/mayswind/AriaNg/releases/download/0.3.0/aria-ng-0.3.0.zip && \
    unzip aria-ng-0.3.0.zip && \
    rm aria-ng-0.3.0.zip

COPY aria2.conf /root/.aria2/aria2.conf
COPY run.sh /run.sh

RUN chmod +x /run.sh

EXPOSE 80
EXPOSE 6800

WORKDIR /data

ENV RPC_SECRET=yourtoken
ENV ALL_PROXY=

CMD [ "/run.sh" ]
