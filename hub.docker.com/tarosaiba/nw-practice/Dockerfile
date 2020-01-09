FROM nginx

RUN set -x \
    && apt-get update \
    && apt-get install --no-install-recommends --no-install-suggests -y tcpdump telnet iputils-ping net-tools inetutils-traceroute curl

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
