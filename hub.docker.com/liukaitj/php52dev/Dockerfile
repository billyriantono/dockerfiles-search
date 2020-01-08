FROM liukaitj/php52

# install libssl 0.9.8
COPY libssl0.9.8_0.9.8o-4squeeze14_amd64.deb /tmp/
RUN dpkg -i /tmp/libssl0.9.8_0.9.8o-4squeeze14_amd64.deb && \
    rm -f /tmp/libssl0.9.8_0.9.8o-4squeeze14_amd64.deb

# install ZendDebugger
COPY ZendDebugger.so /usr/local/etc/php/

RUN echo 'short_open_tag = On' >> /usr/local/etc/php/php.ini
RUN echo 'zend_extension=/usr/local/etc/php/ZendDebugger.so' >> /usr/local/etc/php/php.ini
RUN echo 'zend_debugger.allow_hosts=0.0.0.0/0' >> /usr/local/etc/php/php.ini
RUN echo 'zend_debugger.expose_remotely=always' >> /usr/local/etc/php/php.ini

EXPOSE 9000 10137
