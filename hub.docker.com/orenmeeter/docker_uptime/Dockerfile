#==================== Building Stage ================================================ 

# Create the image based on the official Node 8.9.0 image from Dockerhub
FROM node:8.11.0 as node

# Create a directory where our app will be placed. This might not be necessary
RUN mkdir -p /uptime_webapp_frontend

# Change directory so that our commands run inside this new directory
WORKDIR /uptime_webapp_frontend

# Copy dependency definitions
COPY package.json /uptime_webapp_frontend

# Install dependencies using npm
RUN npm install

# Get all the code needed to run the app
COPY . /uptime_webapp_frontend

# Expose the port the app runs in
EXPOSE 3000


# #Build the app
# RUN npm run build

# # # start app
CMD ["npm", "start"]

# #==================== Setting up stage ==================== 
# # Create image based on the official nginx - Alpine image
# FROM nginx:1.13.7-alpine

# # COPY --from=node /uptime_webapp_frontend/dist/ /usr/share/nginx/html

# COPY ./nginx.conf /etc/nginx/conf.d/default.conf
