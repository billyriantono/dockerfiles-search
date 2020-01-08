# Download from docker cloud of teatime(public)
FROM teatime/docker-img-django:latest

RUN groupadd -r django && useradd -r -g django django

ADD . /code
RUN chown -R django /code

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh \
    && chown django /entrypoint.sh

COPY entrypoint_web.sh /usr/local/bin/entrypoint_web.sh
RUN chmod +x /usr/local/bin/entrypoint_web.sh \
    && chown django /usr/local/bin/entrypoint_web.sh \
    && ln -s /usr/local/bin/entrypoint_web.sh

WORKDIR /code

ENTRYPOINT ["/entrypoint.sh"]