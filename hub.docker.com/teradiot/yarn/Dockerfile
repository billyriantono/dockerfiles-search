FROM node:7.3.0

ENV YARN_VERSION 0.18.1
RUN curl --silent -o- -L https://yarnpkg.com/install.sh | bash -s -- --version $YARN_VERSION
ENV PATH /root/.yarn/bin:$PATH

ENTRYPOINT yarn
