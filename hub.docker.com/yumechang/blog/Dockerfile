FROM yumechang/apache24_php73

# session to redis run
RUN echo 'session.save_handler = redis\n\
session.save_path = "tcp://redis:6379"\n' >> /usr/local/etc/php/php.ini
