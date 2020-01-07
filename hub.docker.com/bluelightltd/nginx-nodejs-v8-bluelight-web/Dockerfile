FROM nginx

RUN apt update && apt -y install curl gnupg make gcc g++

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -

#RUN apt -y install nodejs npm build-essential
RUN apt -y install npm 




RUN mkdir -p /opt/theme/node_modules

ADD theme /opt/theme/

RUN cd /opt/theme/ && \
    npm install gulp -g && \
    npm install && \
    gulp sass 