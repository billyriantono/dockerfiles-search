
FROM ruby:2.6-slim-stretch

ENV LANG C.UTF-8

# Install deps
RUN apt-get update
RUN apt-get install --no-install-recommends -qy build-essential git
RUN apt-get install --no-install-recommends -qy python3.5 python3-dev python3-pip python3-setuptools

# prepare rootfs
RUN git clone https://github.com/minlearn/jupyter-book-corrected /app \
    # install jupyter-book
    && cd /app \
    && pip3 install numpy jsonschema ipython jupyter_client \
    && python3.5 setup.py install \
    # prepare book src and deps
    && mkdir -p /app/books \
    && cd /app/books \
    && jupyter-book create mybook --demo \
    && cd /app/books/mybook \
    && make install \
    # make run.sh executable
    && cp /app/run.sh /usr/local/bin \
    && chmod +x /usr/local/bin/run.sh
    
# fire it,go
ENV PYTHONIOENCODING=utf-8
VOLUME /app/books
EXPOSE 4000

WORKDIR /app/books
ENTRYPOINT ["run.sh"]
