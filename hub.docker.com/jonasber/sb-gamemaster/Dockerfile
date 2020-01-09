FROM node:alpine
ADD ./app /gamemaster/app/
ADD tsconfig.json /gamemaster/.
# ADD ./build /gamemaster/build/
ADD ./package.json /gamemaster/.
ADD ./package-lock.json /gamemaster/.
WORKDIR /gamemaster
RUN npm install
RUN npm run build
CMD npm start
EXPOSE 3000
