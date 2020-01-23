FROM bluelightltd/nginx-nodejs-v8:latest

RUN mkdir /opt/theme

ADD theme /opt/theme/

RUN cd /opt/theme/default/tools && \
    npm install --global npm@latest && \
    npm install --global yarn && \
    npm install --global gulp-cli && \
    yarn install && \
    gulp 

# CMD ["/bin/bash"]