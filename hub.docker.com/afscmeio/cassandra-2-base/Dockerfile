# copied from official cassandra image for adaptation to CentOS:7
FROM afscmeio/java-8-base
MAINTAINER AFSCME DevOps <devops@afscme.io>

# add additional software first
RUN yum -y install deltarpm \
 && yum -y install ca-certificates curl less net-tools unzip util-linux \
 && yum -y update \
 && yum -y clean all

# environment
ENV GOSU_VER=1.9 \
    GOSU_ARCH=amd64 \
    GOSU_PATH=https://github.com/tianon/gosu/releases/download \
    CASSANDRA_USER=cassandra \
    CASSANDRA_UID=1002 \
    CASSANDRA_VER=2.2.6 \
    MX4J_PATH=http://downloads.sourceforge.net/sourceforge/mx4j \
    MX4J_VER=3.0.2
#
ENV DSC_PKG_NAME=${CASSANDRA_USER}22-${CASSANDRA_VER}-1 \
    CASSANDRA_ETC=/etc/${CASSANDRA_USER} \
    CASSANDRA_DATA=/var/lib/${CASSANDRA_USER} \
    MX4J_TAG=mx4j-${MX4J_VER}
#
ENV CASSANDRA_CONFIG=${CASSANDRA_ETC}/conf \
    DSC_PACKAGE=${DSC_PKG_NAME}.noarch.rpm \
    MX4J_FILE=${MX4J_TAG}.zip

# explicitly set user/group IDs
RUN groupadd -r ${CASSANDRA_USER} --gid=${CASSANDRA_UID} \
 && useradd -r -g ${CASSANDRA_USER} --uid=${CASSANDRA_UID} -G users ${CASSANDRA_USER}

# grab gosu for easy step-down from root
# !! GPG KEY FETCH NOT WORKING !!
##>>RUN gpg --keyserver pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
##>> && curl --silent -o /usr/local/bin/gosu -SL "${GOSU_PATH}/${GOSU_VER}/gosu-${GOSU_ARCH}" \
##>> && curl --silent -o /usr/local/bin/gosu.asc -SL "${GOSU_PATH}/${GOSU_VER}/gosu-${GOSU_ARCH}.asc" \
##>> && gpg --verify /usr/local/bin/gosu.asc \
##>> && rm -Rf /usr/local/bin/gosu.asc /root/.gnupg/ \
##>> && chmod +x /usr/local/bin/gosu
# unchecked but functioning
RUN curl --silent -o /usr/local/bin/gosu -SL "${GOSU_PATH}/${GOSU_VER}/gosu-${GOSU_ARCH}" \
 && chmod +x /usr/local/bin/gosu

# install the datastax repo gpg-key, repo, cassandra
RUN rpm --import "http://rpm.datastax.com/rpm/repo_key" \
 && echo -e "[datastax]\nname=DataStax\ Repo\ for\ Apache\ Cassandra\nbaseurl=http://rpm.datastax.com/community\nenabled=1\ngpgcheck=1\n" > /etc/yum.repos.d/datastax.repo \
 && yum -y install ${DSC_PKG_NAME}

# https://issues.apache.org/jira/browse/CASSANDRA-11661
RUN sed -ri 's/^(JVM_PATCH_VERSION)=.*/\1=25/' ${CASSANDRA_CONFIG}/cassandra-env.sh

RUN mkdir -p "${CASSANDRA_DATA}" "${CASSANDRA_ETC}" \
	&& chown -R "${CASSANDRA_USER}"."${CASSANDRA_USER}" "${CASSANDRA_DATA}" "${CASSANDRA_ETC}" \
	&& chmod -R 775 "${CASSANDRA_DATA}" "${CASSANDRA_ETC}"

#
# add mx4j
#  && cp -a /tmp/${MX4J_TAG}/lib/mx4j*.jar /usr/share/cassandra/lib/ \
#
RUN curl --silent --retry 3 -SLo /tmp/${MX4J_FILE} ${MX4J_PATH}/${MX4J_FILE} \
 && unzip -oqq /tmp/${MX4J_FILE} -d /tmp/ \
 && cp -a /tmp/${MX4J_TAG}/lib/mx4j-tools.jar /usr/share/cassandra/lib/ \
 && chown ${CASSANDRA_USER}.${CASSANDRA_USER} /usr/share/cassandra/lib/mx4j*.jar

VOLUME "${CASSANDRA_DATA}"
COPY docker-entrypoint.sh /docker-entrypoint.sh
#
ENTRYPOINT ["/docker-entrypoint.sh"]

# 7000: intra-node communication
# 7001: TLS intra-node communication
# 7199: JMX
# 8081: MX4J
# 9042: CQL
# 9160: thrift service
EXPOSE 7000 7001 7199 8081 9042 9160
#
CMD ["cassandra", "-f"]
##>>CMD ["/bin/bash"]
