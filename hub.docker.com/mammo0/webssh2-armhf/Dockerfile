FROM mammo0/armv7hf-debian-qemu AS armBin

FROM arm32v6/node:8-alpine
COPY --from=armBin /usr/bin/cross-build-start /usr/bin/
COPY --from=armBin /usr/bin/cross-build-end /usr/bin/
COPY --from=armBin /usr/bin/qemu-arm-static /usr/bin/
COPY --from=armBin /usr/bin/resin-xbuild /usr/bin/

RUN [ "cross-build-start" ]
WORKDIR /usr/src
COPY app/ /usr/src/
RUN npm install --production
RUN [ "cross-build-end" ]

EXPOSE 2222
CMD npm run start
