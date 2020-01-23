FROM fernandoenzo/debian:10s-std
MAINTAINER Fernando Enzo Guarini (fernandoenzo@gmail.com)

ENV DISPLAY :0
EXPOSE 8080/tcp

COPY scripts/ /tmp/scripts
RUN bash /tmp/scripts/basics

CMD ["/usr/share/phpstorm/bin/phpstorm.sh"]
