# Set the base image to node
FROM rethinkdb:latest

MAINTAINER Max Campbell <maxc@maxc.in>


RUN apt-get update
RUN apt-get install -y netcat

# Run app using npm

CMD ["rethinkdb", "--bind", "all"]
