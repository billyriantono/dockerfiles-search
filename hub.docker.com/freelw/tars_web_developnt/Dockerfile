FROM free9080/padavan-ng-build as builder

MAINTAINER Richard Xie

ADD . /opt

RUN mkdir /dist \
	&&	mv /home/toolchain-mipsel/out /opt/toolchain/ \
	&& cd /opt/trunk/ \
	&& ./build_firmware.sh \
	&& cp /opt/trunk/images/*.trx /dist/


FROM alpine

VOLUME [ "/data" ]

WORKDIR /dist

COPY --from=builder /dist /dist