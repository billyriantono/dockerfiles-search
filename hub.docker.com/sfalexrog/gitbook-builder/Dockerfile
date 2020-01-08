FROM node:11.6.0-stretch

RUN npm install gitbook-cli -g \
    && gitbook -V

COPY scripts /scripts

CMD ["/scripts/build_book.sh"]
