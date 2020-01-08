FROM land007/node:latest

MAINTAINER Yiqiu Jia <yiqiujia@hotmail.com>

#RUN apt-get update && apt-get install -y libcairo2-dev libjpeg-dev libpango1.0-dev libgif-dev build-essential g++ python && apt-get clean
RUN apt-get update && apt-get install -y libcairo2-dev libjpeg-dev libpango1.0-dev libgif-dev build-essential g++ && apt-get clean
RUN . $HOME/.nvm/nvm.sh && cd / && npm install canvas

RUN echo $(date "+%Y-%m-%d_%H:%M:%S") >> /.image_times
RUN echo $(date "+%Y-%m-%d_%H:%M:%S") > /.image_time
RUN echo "land007/node-canvas" >> /.image_names
RUN echo "land007/node-canvas" > /.image_name


#docker stop node-canvas ; docker rm node-canvas ; docker run -it --privileged -p 8081:8081 --name node-canvas land007/node-canvas:latest
