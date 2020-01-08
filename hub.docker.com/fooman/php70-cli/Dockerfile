FROM tklx/base:0.1.1
ADD https://www.dotdeb.org/dotdeb.gpg dotdeb.gpg
RUN echo "deb http://packages.dotdeb.org jessie all" > /etc/apt/sources.list.d/dotdeb.list \
    && apt-key add dotdeb.gpg \
    && apt-get update \
    && apt-get --no-install-recommends -y install php7.0-cli\
    && apt-clean --aggressive
CMD ["php","-v"]
