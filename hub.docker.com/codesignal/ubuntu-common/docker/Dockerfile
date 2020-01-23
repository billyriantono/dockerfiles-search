FROM ubuntu:14.04
ENV UPDATE_AT 20171205
RUN apt-get update
RUN sudo apt-get update
RUN apt-get install -y redis-server
CMD ["redis-server"]
EXPOSE 6379

