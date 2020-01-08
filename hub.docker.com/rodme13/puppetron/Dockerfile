FROM cheeaun/puppeteer:1.1.1
COPY . /app
RUN cd /app && yarn --production --pure-lockfile
WORKDIR /app
ENV PORT 80
EXPOSE 80
#CMD yarn start
ENTRYPOINT [ "yarn" ]
CMD ["start"]
