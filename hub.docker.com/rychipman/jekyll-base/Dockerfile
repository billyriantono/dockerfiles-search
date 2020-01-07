FROM rychipman/nginx

RUN apt-get install -y nodejs && \
    apt-get install -y ruby ruby-dev ruby-bundler && \
    gem install jekyll \
                stylus \
                --no-ri --no-rdoc

ONBUILD ADD . /jekyll

ONBUILD RUN cd /jekyll && \
            jekyll build && \
            rm -rf /var/www/html/* && \
            cp -r _site/* /var/www/html
