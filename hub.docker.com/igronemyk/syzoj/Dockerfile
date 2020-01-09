FROM ubuntu:16.04
RUN apt update \
    && apt install -y curl sudo git \
    && git clone https://github.com/Igronemyk/syzoj-install.git /var/syzoj-install \
    && cd /var/syzoj-install \
    && bash install.sh
ENV LANG=C.UTF-8 TZ=Asia/Shanghai
EXPOSE 5283
CMD ["/sbin/init"]
