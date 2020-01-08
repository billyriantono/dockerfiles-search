FROM nginx AS build
ENV VERSION="1.0" \
    AUTHOR="dingxiang"
COPY ./script/EntryPoint.sh /usr/local/bin/dx.sh
COPY ./conf/index.html /usr/share/nginx/html/index.html
COPY ./bin/gosu /usr/local/bin/gosu
COPY ./bin/busybox-x86_64 /usr/local/bin/busybox
VOLUME /usr/share/nginx/html
VOLUME /etc/nginx/
WORKDIR /root
RUN  chmod +x /usr/local/bin/dx.sh && \
     chmod +x /usr/local/bin/gosu && \
     chmod +x /usr/local/bin/busybox && \
     ln -s /usr/local/bin/busybox /bin/wget && \
     ln -s /usr/local/bin/busybox /bin/nc && \
     ln -s /usr/local/bin/busybox /bin/netstat && \
     ln -s  /usr/local/bin/busybox /bin/ps  
EXPOSE 80
ENTRYPOINT ["/usr/local/bin/dx.sh"]
CMD ["nginx","-g","daemon off;"]
