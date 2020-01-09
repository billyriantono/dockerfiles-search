FROM node:13-alpine

ENV USER=drake USER_ID=1001 USER_GID=1001


RUN  apk --no-cache add g++ make bash zlib-dev libpng-dev  yarn git \
&& npm install -g laravel-echo-server bower \
&&  rm -fr /var/cache/apk/* 
RUN addgroup --gid "${USER_GID}" "${USER}" \
&&  adduser \
--disabled-password \
--uid ${USER_ID} \
 --home "/home/$USER" \
--ingroup "$USER" \
--shell /bin/sh \
"${USER}"



ENTRYPOINT ["docker/scripts/node.sh"]