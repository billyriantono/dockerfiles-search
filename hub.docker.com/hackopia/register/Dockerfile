FROM node:8.7.0

# Set a working directory
WORKDIR /usr/src/app

# Copy application files
COPY . .

# Install dependencies
RUN npm install --quiet

CMD ["npm", "run", "dev"]
EXPOSE 3000
