# go get 명령이 실패함, github 에서 download 실패하는데, 
# stackoverflow에서 ssl 버전이 낮아서 인 것으로 추정되는 글을 찾았음
# openssl 버전을 올려서 test를 해보았지만 실패함

# Pull base image
FROM castis/centos5-legacy

RUN wget https://dl.google.com/go/go1.9.2.linux-amd64.tar.gz; \
  tar -C /usr/local -xzf go1.9.2.linux-amd64.tar.gz; \
  rm go1.9.2.linux-amd64.tar.gz
  
RUN wget https://www.openssl.org/source/openssl-1.0.2o.tar.gz; \
  tar xvfz openssl-1.0.2o.tar.gz; \
  cd openssl-1.0.2o; \
  ./config; \
  make; \
  make install; \
  mv /usr/bin/openssl /usr/bin/openssl-0.9.8e; \
  ln -s /usr/local/ssl/bin/openssl /usr/bin/openssl; \
  cd ..; \
  rm -rf openssl-1.0.2o; \
  rm openssl-1.0.2o.tar.gz  
  
# Set environment variables
ENV PATH $PATH:/usr/local/go/bin

