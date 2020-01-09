FROM aslinwang/node-utils:10

RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN echo 'Asia/Shanghai' > /etc/timezone
RUN dpkg-reconfigure -f noninteractive tzdata

RUN npm i -g fbi

ENTRYPOINT ["tail", "-f", "/dev/null"]