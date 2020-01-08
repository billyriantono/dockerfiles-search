FROM cpmcdaniel/papermc:release-1.2

LABEL maintainer="cpmcdaniel@gmail.com"

COPY with-plugins /usr/local/bin

RUN chmod 755 /usr/local/bin/with-plugins

CMD ["/usr/local/bin/with-plugins", "paper", "run"]
