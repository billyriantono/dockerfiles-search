FROM fernandoenzo/debian:10s-min
MAINTAINER Fernando Enzo Guarini (fernandoenzo@gmail.com)

ENV DISPLAY :0

COPY scripts/ /tmp/scripts
RUN bash /tmp/scripts/basics

CMD ["/usr/share/jd2/JDownloader2"]
