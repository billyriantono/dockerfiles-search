# https://github.com/jarun/googler

FROM python:3.8

RUN curl -o /usr/local/bin/googler https://raw.githubusercontent.com/jarun/googler/master/googler && \
    chmod +x /usr/local/bin/googler

ENTRYPOINT ["googler"]
