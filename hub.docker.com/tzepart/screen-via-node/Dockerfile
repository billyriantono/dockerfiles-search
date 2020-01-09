FROM node:6

# Bundle app source
COPY . /src

# Install
RUN cd /src && npm install

EXPOSE  8080

CMD cd /src && node app.js --url=$PAGE_URL --selector=$ELEMENT_SELECTOR --output=$OUTPUT_NAME