FROM ubuntu:14.04
MAINTAINER David Aparicio "david.aparicio@free.fr"

# Install nodejs
RUN apt-get update && apt-get install -qy git build-essential nodejs npm

# Install Tree build dependencies.
RUN apt-get -qy install libicu-dev

# Don't be root.
RUN useradd -m user
USER user
ENV HOME /home/user
WORKDIR /home/user

# Download Tree's source code.
RUN git clone https://github.com/garden/tree.git
WORKDIR tree

# Build Tree.
RUN make links
RUN npm install

#Expose ports.
EXPOSE 8080

#Set the default run command.
CMD ["nodejs", "app", "8080"]
