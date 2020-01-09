FROM referup/inca-nginx:dev

RUN \
  test -f /etc/nginx/conf.d/upstream.conf && \
  rm -vf /etc/nginx/conf.d/upstream.conf 

COPY conf/nginx/conf.d/upstream.conf /etc/nginx/conf.d
# Disable php in this image to ensure no one executes it by error
RUN mv -v /usr/bin/php /usr/bin/php.disabled
