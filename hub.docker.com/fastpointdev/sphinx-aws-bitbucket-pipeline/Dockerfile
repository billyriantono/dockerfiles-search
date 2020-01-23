FROM alpine:latest

RUN apk --update add py-pip && \
    apk --update add -t deps git gcc libjpeg-turbo-dev musl-dev python-dev zlib-dev make && \
    pip install -U sphinx==1.8.3 Pygments setuptools docutils mkdocs mock awscli pillow sphinx_fontawesome \
    git+https://github.com/rtfd/readthedocs-sphinx-ext.git \
    sphinx-rtd-theme alabaster \
    commonmark git+https://github.com/rtfd/recommonmark.git \
    git+https://github.com/mgaitan/sphinxcontrib-mermaid.git && \
    apk del --purge deps && \
    rm -rf /root/.cache /var/cache/apk/*

CMD /bin/sh