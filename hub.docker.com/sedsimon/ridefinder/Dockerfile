FROM node:8

# create user
RUN useradd --user-group --create-home --shell /bin/false app &&\
  npm install --global npm

# create home dir, install app dependencies and switch to app user
ENV HOME=/home/app
COPY --chown=app:app package.json npm-shrinkwrap.json $HOME/ridefinder/

USER app
WORKDIR $HOME/ridefinder
RUN npm install

CMD [ "npm", "run", "dev" ]
