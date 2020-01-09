FROM node

#RUN git config --global url."https://github.com/".insteadOf git@github.com:
RUN git config --global url."https://".insteadOf git://
RUN npm install --save tui-editor
RUN mkdir /site

COPY ./site /site/

WORKDIR /site

RUN npm install

CMD npm start