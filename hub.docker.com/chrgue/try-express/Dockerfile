FROM node:5.9.0
WORKDIR /app
ADD . .

ENV DEBUG=express_app:*
RUN npm install
EXPOSE 3000
CMD npm start

