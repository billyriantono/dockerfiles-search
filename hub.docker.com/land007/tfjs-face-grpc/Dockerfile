FROM land007/tfjs-face:latest
MAINTAINER Yiqiu Jia <yiqiujia@hotmail.com>

RUN . $HOME/.nvm/nvm.sh && cd / && npm install grpc @grpc/proto-loader

RUN echo $(date "+%Y-%m-%d_%H:%M:%S") >> /.image_times
RUN echo $(date "+%Y-%m-%d_%H:%M:%S") > /.image_time
RUN echo "land007/tfjs-face-grpc" >> /.image_names
RUN echo "land007/tfjs-face-grpc" > /.image_name

#docker kill tfjs-face-grpc ; docker rm tfjs-face-grpc ; docker run -it --restart always --privileged -v ~/docker/tfjs-face-grpc:/node -p 80:80 --name tfjs-face-grpc land007/tfjs-face-grpc:latest
#docker kill tfjs-face-grpc ; docker rm tfjs-face-grpc ; docker run -it --restart always --privileged -p 80:80 -p 50050:50050 -p 50051:50051 -p 50052:50052 -p 50053:50053 -p 20022:20022 --name tfjs-face-grpc land007/tfjs-face-grpc:latest
