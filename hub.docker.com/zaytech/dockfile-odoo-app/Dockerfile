FROM ubuntu:14.04
MAINTAINER Leandro Augusto <leandro@zaytech.com.br>

# Exporta usuarios
ENV USER odoo
ENV PASSWORD odoo

# Configura localizacao
RUN locale-gen pt_BR.UTF-8
RUN update-locale LANG=pt_BR.UTF-8

# Instala pacotes basicos
ADD apt_defaults.pgks /tmp/apt_defaults.pgks
RUN apt-get -qq update
RUN apt-get -qq dist-upgrade
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y -q $(cat /tmp/apt_defaults.pgks)

# Instala requisitos apt
ADD apt_prerequisito_odoo.pgks /tmp/apt_prerequisito_odoo.pgks
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y -q $(cat /tmp/apt_prerequisito_odoo.pgks)

# Install ntp e configura localizacao
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y -q ntp
RUN echo "server a.ntp.br" >> /etc/ntp.conf
RUN echo "server b.ntp.br" >> /etc/ntp.conf
RUN echo "server c.ntp.br" >> /etc/ntp.conf

RUN ln -sf /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime
RUN echo "America/Sao_Paulo" > /etc/timezone
RUN dpkg-reconfigure -f noninteractive tzdata

# Configura ssh
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y -q openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:zayth123' |chpasswd
RUN sed -i "s/PermitRootLogin without-password/PermitRootLogin yes/g" /etc/ssh/sshd_config
RUN echo "HISTTIMEFORMAT='|  $USER  |  %F  |  %H:%M:%S  |  '" >> /root/.bashrc


# Adiciona user e baixa repositorios
RUN adduser --system --home=/opt/odoo --group odoo

USER odoo
RUN mkdir /opt/odoo/addons
RUN mkdir /opt/odoo/addons/outros
RUN mkdir /opt/odoo/etc
RUN mkdir /opt/odoo/local
RUN mkdir /opt/odoo/local/sped
ADD odoo8.cfg /opt/odoo/etc/odoo8.cfg

WORKDIR /opt/odoo/
RUN git clone https://github.com/OCA/OCB -b 8.0 --depth 1 server

WORKDIR /opt/odoo/addons
RUN git clone https://github.com/OCA/server-tools -b 8.0 --depth 1
RUN git clone https://github.com/odoo-brazil/account-fiscal-rule.git -b 8.0 --depth 1
RUN git clone https://github.com/odoo-brazil/l10n-brazil.git -b 8.0 --depth 1
RUN git clone https://github.com/odoo-brazil/odoo-brazil-eletronic-documents -b 8.0 --depth 1
RUN git clone https://github.com/Trust-Code/trust-addons -b 8.0 --depth 1
RUN git clone https://github.com/odoo-brazil/odoo-brazil-hr.git -b 8.0 --depth 1
RUN git clone https://github.com/kmee/odoo-brazil-banking.git -b feature/boleto-sem-registro-pyboleto --depth 1
WORKDIR /opt/odoo/addons/outros
RUN git clone https://github.com/wagnerpereirasp/bgi-viacep.git --depth 1 

# Instala pips requerimentos
USER root
WORKDIR /tmp
ADD requirements2.txt /tmp/requirements2.txt
ADD wkhtmltox-0.12.2.1_linux-trusty-amd64.deb /tmp/wkhtmltox-0.12.2.1_linux-trusty-amd64.deb
RUN pip install -r /opt/odoo/server/requirements.txt
RUN pip install -r /tmp/requirements2.txt
RUN dpkg -i /tmp/wkhtmltox-0.12.2.1_linux-trusty-amd64.deb


# Install systemd script
ADD systemd-odoo.conf /etc/init.d/odoo
RUN update-rc.d -f odoo defaults

# Instalar NGinx
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y -q nginx
ADD nginx-odoo /etc/nginx/sites-enabled/nginx-odoo
RUN rm -rf /etc/nginx/sites-enabled/default

# Install supervisor
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y -q supervisor
ADD supervisord.conf /etc/supervisor/conf.d/

# Configura volume e port
VOLUME ["/opt/odoo"]
EXPOSE 80

CMD ["/usr/bin/supervisord"]
