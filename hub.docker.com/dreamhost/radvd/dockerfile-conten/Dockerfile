FROM dragzone/tini:latest

RUN apt-get update -q && \
  apt upgrade -y && \
  DEBIAN_FRONTEND=noninteractive && \
  apt-get install -qy nginx && \
  apt autoremove -y && \
  apt-get clean && \
  rm -rf /var/lib/apt

CMD ["nginx", "-g", "daemon off;"]