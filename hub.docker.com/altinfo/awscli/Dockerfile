FROM fedora
LABEL maitainer="Luiz Fernando Pereira <luizfernandopereira@outlook.com.br>"

RUN dnf install python groff -y \
    && dnf clean all -y \
    && pip install awscli

ENV TIMEZONE=America/Sao_Paulo
RUN ln -snf /usr/share/zoneinfo/$TIMEZONE /etc/localtime && echo $TIMEZONE > /etc/timezone

ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /sbin/tini
RUN chmod +x /sbin/tini

ADD "entrypoint.sh" "/entrypoint.sh"
RUN chmod +x /entrypoint.sh

WORKDIR /app

ENTRYPOINT ["/entrypoint.sh"]

CMD ["aws"]