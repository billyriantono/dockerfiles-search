FROM alpine:edge

LABEL maintainer="Thomas"

RUN apk --update --no-cache add \
	ca-certificates \
	aircrack-ng	

ENTRYPOINT [ "aircrack-ng" ]

CMD [ "--help" ]
