FROM alpine:3.7

RUN apk add --update \
        bash \
        curl \
        python2 \
        python2-dev \
        python3 \
        python3-dev
        
RUN curl https://bootstrap.pypa.io/get-pip.py | python3 && \
    curl https://bootstrap.pypa.io/get-pip.py | python && \
    pip3 install pylint && \
    pip install pylint

COPY pylint2 pylint3 /usr/local/bin/

CMD ["/bin/bash"]

