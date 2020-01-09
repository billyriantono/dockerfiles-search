#FROM centos:6.8
FROM walkonthemarz/pa_base:latest

MAINTAINER walkonthemarz@gmail.com

COPY kfb_reader/libImageOperationLib.so /usr/local/lib
COPY tmap_reader/libiViewerSDK.so /usr/local/lib
    
COPY kfb_reader/50-kfb_reader.ini /etc/php.d/50-kfb_reader.ini
COPY tmap_reader/50-tmap_reader.ini /etc/php.d/50-tmap_reader.ini
COPY kfb_reader /root/kfb_reader
COPY tmap_reader /root/tmap_reader

RUN cd /root/kfb_reader && phpize && ./configure && make && make install \
    && cd /root && rm -rf /root/kfb_reader \
    && cd /root/tmap_reader && phpize && ./configure && make && make install \
    && cd /root && rm -rf /root/tmap_reader


#HEALTHCHECK --interval=5s --timeout=3s CMD curl -fs http://localhost || exit 1
EXPOSE 80
CMD []
#ENTRYPOINT ["/opt/rh/httpd24/root/usr/sbin/apachectl", "-D", "FOREGROUND"]
ENTRYPOINT ["/bin/bash"]
