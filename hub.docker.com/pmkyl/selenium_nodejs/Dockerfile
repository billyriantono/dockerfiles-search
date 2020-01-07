#
# Scala, sbt and Node Dockerfile
#
# https://github.com/pmkyl/sbt-scala-node
#

# Pull base image
FROM selenium/standalone-chrome

RUN sudo apt-get update

RUN sudo apt-get install curl software-properties-common -y

RUN curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -

# Define working directory
RUN sudo apt-get install nodejs

CMD [ "node" ]