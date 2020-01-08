FROM hypercloud/nodejs-base

WORKDIR /app

ONBUILD ADD /app /app
# Run `npm install` in the host machine, copy into the container
# ONBUILD RUN npm install

EXPOSE 8080
CMD []
ENTRYPOINT ["/nodejs/bin/npm", "start"]
