FROM riverhsieh/nodejs

WORKDIR /home

RUN git clone https://github.com/shrikrishnaholla/code.it.git

WORKDIR code.it

RUN git submodule update --init --recursive

RUN npm install

EXPOSE 8000

WORKDIR /home

CMD ["/usr/local/bin/node", "/home/code.it/app.js"]
