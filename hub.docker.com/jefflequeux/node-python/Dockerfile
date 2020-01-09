FROM node:12.7.0-alpine

RUN mkdir /usr/packages
COPY ./binding.node /usr/packages/linux-x64-72/

ENV SASS_BINARY_PATH /usr/packages/linux-x64-72/binding.node

RUN npm cache verify
RUN mkdir /root/.npm/node-sass
RUN mkdir /root/.npm/node-sass/4.12.0
RUN cp /usr/packages/linux-x64-72/binding.node /root/.npm/node-sass/4.12.0/binding.node

RUN apk add --no-cache python && \
    python -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip install --upgrade pip setuptools && \
    rm -r /root/.cache

	
ENTRYPOINT ["sh"]