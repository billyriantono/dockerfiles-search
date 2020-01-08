FROM mkenney/npm:alpine

RUN cd / && \
    git clone https://github.com/gutnikov/webrtc-shooter.git && \
    cd webrtc-shooter && \
    npm i

WORKDIR /webrtc-shooter
VOLUME  /webrtc-shooter
EXPOSE 8080

CMD sh -c "/run-as-user npm run signalling & /run-as-user npm run http"
