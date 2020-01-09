FROM windurst/docker-glibc:2.18
ENV GAME_UPDATE 2019-09-07
ENV GAME_NAME 'factorio'
ENV GAME_VERSION "0.17.68"
WORKDIR /
ENV GAME_PATH '/factorio/bin/x64/'
RUN wget https://www.factorio.com/get-download/${GAME_VERSION}/headless/linux64
RUN tar -xvf linux64
WORKDIR ${GAME_PATH}
ENTRYPOINT ["./factorio"]
CMD ["--start-server", "/factorio/map/map.zip"]
