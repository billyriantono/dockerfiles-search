FROM fedora:22



RUN dnf -y groupinstall 'Xfce Desktop' && \
    dnf -y install \
    supervisor \
    xrdp \
    && dnf clean all

ADD https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm /tmp/

RUN dnf -y install /tmp/google-chrome-stable_current_x86_64.rpm  && dnf clean all


RUN useradd foo && \
    echo foo:bar | chpasswd

# http://sigkillit.com/2013/02/26/how-to-remotely-access-linux-from-windows/
COPY etc/ /etc/

# Allow all users to connect via RDP.
RUN sed -i '/TerminalServerUsers/d' /etc/xrdp/sesman.ini && \
    sed -i '/TerminalServerAdmins/d' /etc/xrdp/sesman.ini

EXPOSE 3389
CMD ["supervisord", "-n"]
