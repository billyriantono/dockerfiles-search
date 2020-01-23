FROM alpine

ENV RPC_SECRET=

RUN mkdir -p /opt/aria2/admin && \
      mkdir /opt/aria2/downloads && \
      mkdir -p /run/nginx && \
      apk add --update aria2 git nginx && \
      git clone https://github.com/mayswind/AriaNg-DailyBuild.git /opt/aria2/admin && \
      apk del git

COPY nginx.conf /etc/nginx/      
COPY ./entrypoint.sh /opt/aria2/

EXPOSE 80
EXPOSE 6800

ENTRYPOINT ["sh", "/opt/aria2/entrypoint.sh"]
