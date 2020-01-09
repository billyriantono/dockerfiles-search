# Use an official Python runtime as a parent image
FROM node

# Set the working directory to /app
WORKDIR /meteocityserveurweb

# Copy the current directory contents into the container at /app
COPY . /meteocityserveurweb

ADD webclient/index.html .
ADD webclient/css/meteocity.css ./css/meteocity.css
ADD webclient/js/logic.js ./js/logic.js
ADD webclient/js/config.js ./js/config.js
ADD webclient/js/villeselect.js ./js/villeselect.js
ADD webclient/img/aucun.png ./img/aucun.png
ADD webclient/img/compile.png ./img/compile.png
ADD webclient/img/pass.png ./img/pass.png
ADD webclient/img/fail.png ./img/fail.png
ADD webclient/img/meteocity.png ./img/meteocity.png


# Install any needed packages specified in requirements.txt
RUN npm install -g http-server

# Run node app when the container launches
CMD ["http-server", "-s", "-c-1", "-p 7780"]