FROM node:8

# Create app directory
WORKDIR /usr/src/app
	
# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./

# If you are building your code for production
# RUN npm install --only=production
RUN npm install

# ENV instruction sets the environment variable 
ENV APP_PORT=8080
ENV DB_HOST=127.0.0.1
ENV DB_PORT=3306
ENV DB_USER=appuser
ENV DB_PASSWORD=apppassword

# Bundle app source
COPY . .

EXPOSE 8080

CMD [ "npm", "start" ]

