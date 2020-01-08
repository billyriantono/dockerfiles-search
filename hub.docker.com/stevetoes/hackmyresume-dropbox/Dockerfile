FROM nouchka/hackmyresume:1.0
MAINTAINER "Steve Toes"

WORKDIR /

RUN curl "https://raw.githubusercontent.com/andreafabrizi/Dropbox-Uploader/master/dropbox_uploader.sh" \
-o /dropbox_uploader.sh && \
chmod +x /dropbox_uploader.sh

COPY upload.sh /upload.sh
RUN chmod +x /upload.sh

CMD /upload.sh
