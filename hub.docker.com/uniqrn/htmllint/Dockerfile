FROM node:latest
LABEL maintainer "unicorn research Ltd"

WORKDIR /root
COPY lint.js /root/lint.js
RUN npm install htmllint

CMD ["/root/lint.js"]
