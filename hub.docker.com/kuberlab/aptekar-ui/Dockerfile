FROM kuberlab/aptekar-ui:base

ADD . /aptekar-ui-base

RUN cd /aptekar-ui-base \
	&& ./build.sh \
	&& cp -R nginx-conf/* /etc/nginx/ \
	&& gulp build \
	&& mkdir -p /www \
	&& cp -R /aptekar-ui-base/dist/* /www/ \
	&& rm -R /aptekar-ui-base

FROM nginx:1.11

COPY --from=0 /etc/nginx /etc/nginx
COPY --from=0 /www /www

EXPOSE 80