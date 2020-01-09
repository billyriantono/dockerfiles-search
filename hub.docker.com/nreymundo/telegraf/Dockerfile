FROM telegraf:alpine

RUN apk add --update python lm_sensors && \
		rm -rf /var/cache/apk/
		
CMD ["telegraf"]