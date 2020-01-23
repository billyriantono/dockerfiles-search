FROM customercentrix/ubuntu

RUN date -u +"%Y-%m-%d %H:%M:%S" && cd /opt \
  && date -u +"%Y-%m-%d %H:%M:%S" && wget http://gwan.com/archives/gwan_linux64-bit.tar.bz2 \
  && date -u +"%Y-%m-%d %H:%M:%S" && tar -xjf gwan_linux64-bit.tar.bz2 \
  && date -u +"%Y-%m-%d %H:%M:%S" && mv gwan_linux64-bit gwan \
  && date -u +"%Y-%m-%d %H:%M:%S" && rm -rf gwan/0.0.0.0_8080/\#0.0.0.0/www \
  && date -u +"%Y-%m-%d %H:%M:%S" && cd /opt \
  && date -u +"%Y-%m-%d %H:%M:%S" && wget https://www.cia.gov/library/publications/download/download-2014/factbook.zip \
  && date -u +"%Y-%m-%d %H:%M:%S" && unzip factbook.zip \
  && date -u +"%Y-%m-%d %H:%M:%S" && mv factbook www \
  && date -u +"%Y-%m-%d %H:%M:%S" && ln -s /opt/www gwan/0.0.0.0_8080/\#0.0.0.0/www 

WORKDIR /opt/gwan
EXPOSE 8080

CMD ./gwan

