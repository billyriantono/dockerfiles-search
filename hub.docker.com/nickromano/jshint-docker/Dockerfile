FROM node:6

RUN npm install -g jshint

RUN mkdir /code
WORKDIR /code

ENTRYPOINT ["jshint"]
CMD ["."]
