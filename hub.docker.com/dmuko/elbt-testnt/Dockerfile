from openjdk:11

add https://dbeaver.io/files/dbeaver-ce_latest_amd64.deb /
run apt-get update && \
  apt-get install -y /dbeaver-ce_latest_amd64.deb && \
  rm -rf /var/lib/apt/lists/* /dbeaver-ce_latest_amd64.deb
