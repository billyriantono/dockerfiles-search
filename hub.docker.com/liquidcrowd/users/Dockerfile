FROM mhart/alpine-node:10.1
RUN node -v
WORKDIR /users
COPY . /users
RUN npm install
EXPOSE 8080
ENTRYPOINT ["node"]
CMD ["server.js"]