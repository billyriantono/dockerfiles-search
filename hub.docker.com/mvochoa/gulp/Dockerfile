FROM node:9

RUN apt-get update -qq && apt-get install -y build-essential
RUN curl -o- -L https://yarnpkg.com/install.sh | bash
ENV LC_CTYPE=en_US.UTF-8
ENV LANG=en_US.UTF-8

RUN mkdir -p /var/gulp
COPY ./gulpfile.js /var/gulp/gulpfile.js
COPY ./package.json /var/gulp/package.json
COPY ./.babelrc /var/gulp/.babelrc
RUN cd /var/gulp && yarn install

WORKDIR /var/gulp
EXPOSE 35729
CMD ["yarn", "start"]