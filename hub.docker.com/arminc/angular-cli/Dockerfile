FROM node:6.9.1

EXPOSE 4200 49152

RUN set -ex;                    \
    npm install -g angular-cli; \
    npm cache clean;

ENTRYPOINT ["ng"]
CMD ["--help"]
