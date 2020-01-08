FROM land007/node:latest

MAINTAINER Yiqiu Jia <yiqiujia@hotmail.com>

RUN apt-get install -y python build-essential

RUN . $HOME/.nvm/nvm.sh && cd / && npm install @tensorflow/tfjs @tensorflow/tfjs-node

RUN echo $(date "+%Y-%m-%d_%H:%M:%S") >> /.image_times
RUN echo $(date "+%Y-%m-%d_%H:%M:%S") > /.image_time
RUN echo "land007/tfjs" >> /.image_names
RUN echo "land007/tfjs" > /.image_name

#docker stop tfjs ; docker rm tfjs ; docker run -it --privileged --name tfjs land007/tfjs-node:latest
