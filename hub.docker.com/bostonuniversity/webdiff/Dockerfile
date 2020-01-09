FROM backstopjs/backstopjs:latest

RUN mkdir /app

COPY package.json /app/package.json
COPY package-lock.json /app/package-lock.json

RUN cd /app ; npm install

COPY init.sh /usr/local/bin/init
RUN chmod u+x /usr/local/bin/init

COPY lib/ /app/lib
COPY default-on-before/ /app/default-on-before/
COPY compare.js auth-cookie.js init.js /app/
RUN chmod u+x /app/compare.js /app/auth-cookie.js /app/init.js

ENTRYPOINT [ "/usr/local/bin/node", "/app/compare.js" ]
