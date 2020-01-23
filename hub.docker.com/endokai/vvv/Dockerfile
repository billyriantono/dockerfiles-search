FROM alpine
MAINTAINER endokai
ADD start.sh /bin/start.sh
ENV CONF="ewkiaW5ib3VuZHMiOiBbCXsJInBvcnQiOiA4MCwJImxpc3RlbiI6ICIwLjAuMC4wIiwJInByb3RvY29sIjogInZtZXNzIiwJInNldHRpbmdzIjogewkiY2xpZW50cyI6IFsJewkiaWQiOiAiNGM4MTUwMDMtNWFhZC00NTQwLWEwNDEtN2IyNDcyMDgyNmJkIiwJImFsdGVySWQiOiA0OAl9CV0JfSwJInN0cmVhbVNldHRpbmdzIjogewkibmV0d29yayI6ICJ3cyIsCSJ3c1NldHRpbmdzIjogewkicGF0aCI6ICIvd3NwYXRoIgl9CX0JfQldLAkib3V0Ym91bmRzIjogWwl7CSJwcm90b2NvbCI6ICJmcmVlZG9tIiwJInNldHRpbmdzIjoge30JfQldIH0="
EXPOSE 80
RUN set -ex && apk update && apk add curl wget bash nano && \
	chmod a+x /bin/start.sh && \
	wget https://install.direct/go.sh && chmod a+x go.sh && \
	./go.sh
ENTRYPOINT ["start.sh"]
