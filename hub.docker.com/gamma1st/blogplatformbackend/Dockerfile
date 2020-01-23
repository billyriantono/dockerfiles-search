FROM node

WORKDIR /usr/src

COPY /src .

WORKDIR /usr

COPY package.json .
COPY tsconfig.build.json .
COPY tsconfig.json .

CMD ["npm", "install"]

CMD ["npm", "run", "build"]
