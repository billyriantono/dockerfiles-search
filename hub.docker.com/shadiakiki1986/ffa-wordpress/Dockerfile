FROM wordpress

#RUN echo "Acquire::http::Proxy \"http://172.17.0.2:3142\";" | tee /etc/apt/apt.conf.d/01proxy \
RUN apt-get -qq update > /dev/null \
    && apt-get -qq -y install git > /dev/null

RUN cd /usr/src/wordpress/wp-content/plugins/ \
    && git clone https://github.com/WP-API/WP-API rest-api \
    && cd rest-api \
    && git checkout tags/2.0-beta15

RUN cd /usr/src/wordpress/wp-content/plugins/ \
    && git clone https://github.com/WP-API/Basic-Auth
