FROM fedora

LABEL maitainer="Luiz Fernando Pereira <luizfernandopereira@outlook.com.br>"

RUN dnf install ansible openssh openssh-clients -y && dnf clean all

ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /sbin/tini
RUN chmod +x /sbin/tini

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

WORKDIR /ansible

ENTRYPOINT ["/bin/sh", "/entrypoint.sh"]

CMD ["ansible"]