FROM node:8.15

RUN apt -y update && apt install -y git 
RUN npm install -g @vue/cli@3.3.0

RUN mkdir /vue-apps
WORKDIR /vue-apps

RUN apt autoremove -y \
	&& apt autoclean -y \
	&& apt clean -y \
	&& rm -rf /ver/lib/apt/lists/*

ARG UI_HOST="127.0.0.1"
ARG UI_PORT=8000

VOLUME [ "/root/.vuerc", "/root/.vue-cli-ui", "/root/.gitconfig" ]

CMD [ "sh", "-c", "vue ui -H $UI_HOST -p $UI_PORT" ]
