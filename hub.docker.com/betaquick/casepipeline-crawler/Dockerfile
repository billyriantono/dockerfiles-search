FROM betaquick/selenium-node
LABEL maintainer="BetaQuick LLC<wale@betaquick.com>"
ADD .  /App
WORKDIR /App
RUN npm install

EXPOSE 4444
CMD ["bash", "start.sh"]
