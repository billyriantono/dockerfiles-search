FROM rychipman/nginx

ADD ./hugo /bin/hugo

ONBUILD ADD . /hugo

ONBUILD RUN cd /hugo && \
            hugo && \
            rm -rf /var/www/html/* && \
            cp -r public/* /var/www/html
