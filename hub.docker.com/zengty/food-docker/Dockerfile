FROM node:10

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app
# Install any needed packages specified in requirements.txt
RUN npm install --prod
RUN npm install pm2 -g

# Make port 80 available to the world outside this container
EXPOSE 4000

# Run app.py when the container launches
CMD ["./wait-for-it.sh", "mysql:3306", "--", "npm", "run", "docker"]