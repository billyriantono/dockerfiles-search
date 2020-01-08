FROM land007/tfjs-html:latest

MAINTAINER Yiqiu Jia <yiqiujia@hotmail.com>

RUN cd /node_ && git clone https://github.com/justadudewhohacks/face-api.js.git
RUN . $HOME/.nvm/nvm.sh && cd /node_/face-api.js/ && npm i && cd /node_/face-api.js/examples/examples-nodejs/ && npm i && npm install -g ts-node && npm install -g typescript
#RUN cd /node_/face-api.js/examples/examples-nodejs/ && tsc *.ts && node faceDetection.js && node faceDetection.js && node faceLandmarkDetection.js && node faceRecognition.js

#ADD face_node /node
#WORKDIR /node
#RUN cp /node_modules/@tensorflow/tfjs-core/dist/io/weights_loader.js /node_modules/@tensorflow/tfjs-core/dist/io/weights_loader_old.js
#ADD weights_loader.js /node_modules/@tensorflow/tfjs-core/dist/io/weights_loader.js
#CMD /etc/init.d/ssh start && node /node/lxp.js

#docker stop face ; docker rm face ; docker run -it --privileged -p 8081:8081 -p 20022:20022 --name face land007/tfjs-face:latest

#docker stop tfjs-face ; docker rm tfjs-face ; docker run -it --privileged -p 18081:8081 -p 20122:20022 --name tfjs-face land007/tfjs-face:latest