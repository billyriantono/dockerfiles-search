FROM adamruzicka/simple_apache
RUN yum install -y php && \
    yum clean all
ADD ./src/* /var/www/html/
