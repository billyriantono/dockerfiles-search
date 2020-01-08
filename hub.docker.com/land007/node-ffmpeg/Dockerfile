FROM land007/node:latest

MAINTAINER Yiqiu Jia <yiqiujia@hotmail.com>

RUN apt-get update && apt-get install -y ffmpeg && apt-get clean

RUN echo $(date "+%Y-%m-%d_%H:%M:%S") >> /.image_times
RUN echo $(date "+%Y-%m-%d_%H:%M:%S") > /.image_time
RUN echo "land007/node-ffmpeg" >> /.image_names
RUN echo "land007/node-ffmpeg" > /.image_name

#docker stop node-ffmpeg ; docker rm node-ffmpeg ; docker run -it --privileged -v ~/docker/node-ffmpeg:/node -p 80:80 --name node-ffmpeg land007/node-ffmpeg:latest
