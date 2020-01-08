FROM land007/node:latest
MAINTAINER Yiqiu Jia <yiqiujia@hotmail.com>

RUN . $HOME/.nvm/nvm.sh && cd / && npm install grpc @grpc/proto-loader

RUN echo $(date "+%Y-%m-%d_%H:%M:%S") >> /.image_times
RUN echo $(date "+%Y-%m-%d_%H:%M:%S") > /.image_time
RUN echo "land007/node-grpc" >> /.image_names
RUN echo "land007/node-grpc" > /.image_name

#docker stop node-grpc ; docker rm node-grpc ; docker run -it --restart always --privileged -v ~/docker/node:/node -p 80:80 --name node-grpc land007/node-grpc:latest
