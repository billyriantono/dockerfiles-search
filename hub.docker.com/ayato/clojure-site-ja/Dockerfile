FROM buildpack-deps:artful

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        openjdk-8-jdk-headless \
        python3.6 \
        po4a \
        unzip

ENV PYTHON_PIP_VERSION 9.0.1

RUN set -ex; \
    \
    wget -O get-pip.py 'https://bootstrap.pypa.io/get-pip.py'; \
    \
    python get-pip.py \
        --disable-pip-version-check \
        --no-cache-dir \
        "pip==$PYTHON_PIP_VERSION" \
    ; \
    pip --version; \
    \
    find /usr/local -depth \
        \( \
            \( -type d -a \( -name test -o -name tests \) \) \
            -o \
            \( -type f -a \( -name '*.pyc' -o -name '*.pyo' \) \) \
        \) -exec rm -rf '{}' +; \
        rm -f get-pip.py

COPY python-packages.txt python-packages.txt

RUN pip install -r python-packages.txt

WORKDIR /tmp

RUN wget -q https://github.com/redpen-cc/redpen/releases/download/redpen-1.9.0/redpen-1.9.0.tar.gz -O - | tar xz \
    && cp -av redpen-distribution-1.9.0/* /usr/local/ \
    && rm -rf redpen-distribution-1.9.0 \
    && wget -q http://cdn.cognitect.com/clojure.org/jbake-2.5.0-SNAPSHOT-bin.zip -O jbake.zip \
    && unzip -o jbake.zip \
    && cp -av jbake-2.5.0-SNAPSHOT/* /usr/local/ \
    && rm -rf jbake-2.5.0-SNAPSHOT
