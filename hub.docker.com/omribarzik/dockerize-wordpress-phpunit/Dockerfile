FROM chriszarate/wordpress-phpunit

# dockerize
ENV DOCKERIZE_RELEASE v0.2.0/dockerize-linux-amd64-v0.2.0.tar.gz
RUN curl -sL https://github.com/jwilder/dockerize/releases/download/${DOCKERIZE_RELEASE} \
    | tar -C /usr/bin -xzvf -
