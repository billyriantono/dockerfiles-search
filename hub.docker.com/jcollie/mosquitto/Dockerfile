FROM registry.fedoraproject.org/fedora:27 AS base

ENV LANG C.UTF-8

RUN dnf -y update

FROM base AS authplug

RUN dnf -y install mosquitto mosquitto-devel openssl-devel openldap-devel git gcc rpm-build

RUN mkdir -p /opt/mosquitto-auth-plug
RUN git clone https://github.com/jpmens/mosquitto-auth-plug.git /opt/mosquitto-auth-plug
COPY config.mk /opt/mosquitto-auth-plug
RUN cd /opt/mosquitto-auth-plug && make

FROM base

RUN dnf -y install mosquitto openssl-libs openldap

RUN mkdir /opt/mosquitto-auth-plug
COPY --from=authplug /opt/mosquitto-auth-plug/np /opt/mosquitto-auth-plug/auth-plug.so /opt/mosquitto-auth-plug/

EXPOSE 1883 8883

VOLUME /etc/mosquitto

USER mosquitto

ENTRYPOINT ["/usr/sbin/mosquitto", "-c", "/etc/mosquitto/mosquitto.conf"]

# Local Variables:
# indent-tabs-mode: nil
# End:
