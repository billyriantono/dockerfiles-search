FROM centos:centos6

# Enable Extra Packages for Enterprise Linux (EPEL) for CentOS
RUN yum install -y epel-release
# Install Node.js and npm
RUN yum install -y nodejs npm

# Install app dependencies
RUN mkdir /src

# Set the working directory for: RUN, CMD, ADD, COPY, ENTRYOINT instructions.
WORKDIR /src
COPY . /src 

RUN npm install 

EXPOSE 3000 

# Start the application
CMD ["npm", "start"]


