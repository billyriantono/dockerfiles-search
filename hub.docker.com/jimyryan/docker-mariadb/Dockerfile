# Debian
# Problem with version 10.1 (on windows, cannot start a container with host directory as /var/lib/mysql mount)
FROM mariadb:10.0 
MAINTAINER JimyRyan

#################################################################################
#################################################################################
#                                                                               #
#                [START :: TIMEZONE, LOCALE & UPDATE / UPGRADE]                 #
#                                                                               #
#################################################################################
RUN set -e \
	&& apt-get update -y \
    && apt-get install -y locales

# Set locale and timezone 
ENV LANGUAGE=fr_FR.UTF-8
ENV LANG=fr_FR.UTF-8
ENV LC_ALL=fr_FR.UTF-8
ENV TZ=Europe/Paris

# Change locale and timezone 
RUN set -e \
    && sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen \
    && sed -i -e 's/# '$LANG' UTF-8/'$LANG' UTF-8/' /etc/locale.gen \
    && locale-gen \
    && update-locale LANG=$LANG \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && echo $TZ > /etc/timezone

# Update distribution
RUN apt-get update -y \
    && apt-get upgrade -y
#################################################################################
#                                                                               #
#                   [END :: TIMEZONE, LOCALE & UPDATE / UPGRADE]                #
#                                                                               #
#################################################################################
#################################################################################

ARG os_target=Windows

# Copy override config file
COPY conf/mysql/*.cnf /etc/mysql/conf.d/
RUN chmod 644 /etc/mysql/conf.d/* \
	&& mkdir -p /var/log/mysql

# Uncomment config OS type if Windows
RUN echo $os_target;
RUN if [ "$os_target" = "Windows" ]; then \
		echo "Set lower_case_table_names=2 (Windows Plateforme)..."; \
		sed -i "s/#lower_case_table_names=2/lower_case_table_names=2/g" /etc/mysql/conf.d/my.cnf; \
	fi
	
VOLUME /var/log/mysql

# Possibility to call the Docker Cloud trigger API for reload in
ENV CALL_API_URL_TRIGGER_WHEN_READY=

# Waiter
ENV DOCKERIZE_VERSION 0.1.0
ENV DOCKERIZE_TIMEOUT 1800
ENV DOCKERIZE_WAIT_SERVICES=
RUN set -xe \
	&& apt-get install -y wget \
	&& wget "https://github.com/jwilder/dockerize/releases/download/v${DOCKERIZE_VERSION}/dockerize-linux-amd64-v${DOCKERIZE_VERSION}.tar.gz" -O /tmp/dockerize-linux-amd64-v${DOCKERIZE_VERSION}.tar.gz \
	&& tar -C /usr/local/bin -xzvf /tmp/dockerize-linux-amd64-v${DOCKERIZE_VERSION}.tar.gz

# Entrypoint & environement variable
COPY /*.sh /
RUN set -e \
	&& chmod 700 /*.sh

ENTRYPOINT ["/my-entrypoint.sh"]

CMD ["mysqld"]