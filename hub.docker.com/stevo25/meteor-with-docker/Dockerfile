FROM stevo25/debian-with-docker-image

RUN apt-get update && apt-get install -y gnupg2 build-essential python \
    && curl https://install.meteor.com/ | sh \
    && meteor npm install -g yarn

CMD ["sh"]