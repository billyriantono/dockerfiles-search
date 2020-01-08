FROM ubuntu:18.04
LABEL maintainer="Doh"
COPY cloudflared .
RUN chmod +x cloudflared && mv cloudflared /bin/
EXPOSE 53/udp
ENTRYPOINT ["cloudflared","proxy-dns","--port","53","--address","0.0.0.0","--upstream","https://1.1.1.1/dns-query","https://1.0.0.1/dns-query"]
#CMD ["cloudflared","proxy-dns","--port","53","--address","0.0.0.0","--upstream","https://1.1.1.1/dns-query","https://1.0.0.1/dns-query"]
#docker run -d --name doh -p 53:53/udp doh