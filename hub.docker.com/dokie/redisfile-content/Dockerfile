FROM ubuntu
RUN apt-get update && apt-get install  -y nodejs npm && \
    update-alternatives --install /usr/bin/node node /usr/bin/nodejs 10 && \
    npm install -y d3 jsdom && \
    apt-get install -y librsvg2-bin &&\
    apt-get install -y imagemagick

CMD ["bash"]
