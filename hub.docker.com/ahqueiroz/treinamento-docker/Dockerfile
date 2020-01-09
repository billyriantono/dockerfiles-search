FROM nginx
MAINTAINER Fernandinho fernandinho@silva.com.br
LABEL Description = Conteiner do curso
LABEL class =Laboratorio
EXPOSE 80
USER root
VOLUME [usrsharenginxhtml]
ARG via_arg=vv
ENV via_env=${via_arg}
RUN apt-get update