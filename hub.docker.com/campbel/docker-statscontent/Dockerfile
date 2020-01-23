FROM node:10.16.3
COPY package*.json ./
#COPY nginx/nginx.conf /etc/nginx/nginx.conf
COPY . .
RUN rm -rf node_modules
RUN rm -rf .next
RUN rm package-lock.json
COPY . /app
WORKDIR  /app
RUN rm -rf node_modules
RUN rm -rf .next
#RUN apk --no-cache add --virtual builds-deps build-base python
RUN npm install
RUN npm rebuild bcrypt --build-from-source
RUN npm audit fix
EXPOSE 3001

# Uncomment for Devlopment
#ENV NODE_ENV development
#CMD ["npm", "run", "dev"]

# Uncomment for Production
ENV NODE_ENV production
#RUN ["npm", "run", "build"]
CMD ["npm", "start"]

