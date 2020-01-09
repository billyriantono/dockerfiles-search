FROM java:8-jre

RUN apt-get update && \
    apt-get install -y \
        curl \
        ruby \
        unzip

RUN useradd -m sencha && \
    cd && cp -R .bashrc .profile /home/sencha && \
    mkdir -p /project && \
    chown -R sencha:sencha /home/sencha /project

USER sencha
ENV HOME /home/sencha

RUN curl -o /home/sencha/cmd.sh.zip http://cdn.sencha.com/cmd/5.1.0.26/SenchaCmd-5.1.0.26-linux-x64.run.zip && \
    unzip -p /home/sencha/cmd.sh.zip > /home/sencha/cmd-install.sh 

USER root

RUN chmod +x /home/sencha/cmd-install.sh 

USER sencha

RUN /home/sencha/cmd-install.sh --prefix /home/sencha/ --mode unattended && \
    rm /home/sencha/cmd*

ENV PATH /home/sencha/Sencha/Cmd/5.1.0.26/:$PATH

VOLUME /project
WORKDIR /project

EXPOSE 1841

COPY entrypoint.sh /

USER root
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
CMD ["help"]