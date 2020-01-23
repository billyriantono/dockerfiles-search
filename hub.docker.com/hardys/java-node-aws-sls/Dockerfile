FROM openjdk:8
MAINTAINER Hardys <hardyscc@gmail.com>

# Do a general update to help downstream container bulids
RUN apt-get clean && apt-get update

# install node
RUN wget -qO- https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs

# install awscli
RUN apt-get install -y awscli

# update npm & install serverless
RUN npm install -g npm serverless

# Add a default Command
CMD ["bash"]
