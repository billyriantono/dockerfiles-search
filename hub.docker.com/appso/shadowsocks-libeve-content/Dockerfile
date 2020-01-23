FROM appimagecrafters/docker-base
RUN yum install -y xz autoconf

COPY --from=appimagecrafters/docker-autoconf /usr/local /usr/local

ADD install-automake.sh /
ARG AUTOMAKE_VERSION=1.16.1
RUN /install-automake.sh