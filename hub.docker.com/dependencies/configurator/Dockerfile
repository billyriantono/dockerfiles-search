FROM python:3.6-alpine

RUN apk --no-cache add git wget

# add a non-root user and give them ownership
RUN adduser -D -u 9000 app && \
    # repo
    mkdir /repo && \
    chown -R app:app /repo && \
    # app code
    mkdir /usr/src/app && \
    chown -R app:app /usr/src/app

RUN pip install pyyaml

WORKDIR /usr/src/app

ENV DEPS_VERSION=2.4.1
RUN wget https://github.com/dependencies-io/deps/releases/download/${DEPS_VERSION}/deps_${DEPS_VERSION}_linux_amd64.tar.gz && \
    mkdir deps && \
    tar -zxvf deps_${DEPS_VERSION}_linux_amd64.tar.gz -C deps && \
    ln -s /usr/src/app/deps/deps /usr/local/bin/deps

# run everything from here on as non-root
USER app

RUN git config --global user.email "bot@dependencies.io" && git config --global user.name "Dependencies.io Bot"

ADD src/ /usr/src/app

WORKDIR /repo

ENTRYPOINT ["python", "/usr/src/app/entrypoint.py"]
