FROM openshift/origin

# Jenkins image for OpenShift
#
# This image provides a Jenkins server, primarily intended for integration with
# OpenShift. Jenkins LTS packages are from https://pkg.jenkins.io/redhat-stable.
#
# Volumes:
# * /var/jenkins_home
# Environment:
# * $JENKINS_PASSWORD - Password for the Jenkins 'admin' user.

# Set a bunch of labels.
LABEL   architecture="x86_64" \
        io.k8s.description="Jenkins" \
        io.k8s.display-name="Jenkins $JENKINS_VERSION" \
        io.openshift.expose-services="8080:http, 50000:https" \
        io.openshift.source-repo-url="https://github.com/raaftech/jenkins" \
        io.openshift.tags="ci,cd,build,jenkins" \
        License="Apache-2.0" \
        maintainer="$MAINTAINER_NAME <$MAINTAINER_EMAIL>" \
        name="jenkins" \
        vendor="Jenkins" \
        version="v$JENKINS_VERSION"

# Set the proxy host and port.
ENV DEBIAN_FRONTEND="noninteractive" \
    GIT_VERSION="2.22.1" \
    HOME="/var/lib/jenkins" \
    JAVA_TOOL_OPTIONS="-XX:+UseConcMarkSweepGC -XX:InitialRAMPercentage=60.0 -XX:MaxRAMPercentage=80.0 -XX:MinHeapFreeRatio=25 -XX:MaxHeapFreeRatio=50 -Dsun.zip.disableMemoryMapping=true" \
    JENKINS_HOME="/var/lib/jenkins" \
    JENKINS_MAIL_HOST="localhost" \
    JENKINS_MAIL_PORT="25" \
    JENKINS_RPM_VERSION="2.190.2-1.1" \
    JENKINS_SHARED_LIBRARY_ENABLED="true" \
    JENKINS_SHARED_LIBRARY_REPOSITORY="https://github.com/raaftech/jenkins.git" \
    JENKINS_SHARED_LIBRARY_CREDENTIALID="none" \
    JENKINS_UC="https://updates.jenkins.io" \
    JENKINS_URL_SCHEME="http" \
    JENKINS_VERSION="2" \
    LANG="en_US.UTF-8" \
    LC_ALL="en_US.UTF-8" \
    LISTENER_PORT="8080" \
    MAINTAINER_NAME="RAAF Technology" \
    MAINTAINER_EMAIL="info@raaf.tech" \
    OPENSHIFT_JENKINS_SETUP_CREDENTIALS="false" \
    OPENSHIFT_JENKINS_IMAGE_VERSION="4.0" \
    OPENSHIFT_SUPPORTED_TEMPLATES="some-template-you-made,some-other-openshift-template" \
    OPENSHIFT_TARGET_PROJECTS="some-dev-project,some-test-project,etc" \
    SONAR_SERVICE_ENABLED="false" \
    SONAR_SERVICE_TOKEN="none" \
    SONAR_SERVICE_URL="http://localhost:9000"

EXPOSE $LISTENER_PORT 50000

RUN yum install -y /usr/bin/applydeltarpm && \
    curl https://pkg.jenkins.io/redhat-stable/jenkins.repo -o /etc/yum.repos.d/jenkins.repo && \
    rpm --import https://pkg.jenkins.io/redhat-stable/jenkins-ci.org.key && \
    yum install -y centos-release-scl-rh && \
    curl https://copr.fedorainfracloud.org/coprs/alsadi/dumb-init/repo/epel-7/alsadi-dumb-init-epel-7.repo -o /etc/yum.repos.d/alsadi-dumb-init-epel-7.repo && \
    #x86_EXTRA_RPMS=$(if [ "$(uname -m)" == "x86_64" ]; then echo -n java-1.8.0-openjdk.i686 java-1.8.0-openjdk-devel.i686 ; fi) && \
    INSTALL_PKGS="gcc dejavu-sans-fonts rsync gettext git tar zip unzip openssl bzip2 dumb-init java-1.8.0-openjdk java-1.8.0-openjdk-devel libcurl-devel gettext-devel openssl-devel perl-CPAN perl-devel zlib-devel" && \
    yum -y --setopt=tsflags=nodocs install $INSTALL_PKGS && \
    # have temporarily removed the validation for java to work around known problem fixed in fedora; jupierce and gmontero are working with
    # the requisit folks to get that addressed ... will switch back to rpm -V $INSTALL_PKGS when that occurs
    rpm -V  gcc dejavu-sans-fonts rsync gettext git tar zip unzip openssl bzip2 dumb-init gettext-devel openssl-devel perl-CPAN perl-devel zlib-devel && \
    yum clean all  && \
    localedef -f UTF-8 -i en_US en_US.UTF-8

ADD https://pkg.jenkins.io/redhat-stable/jenkins-${JENKINS_RPM_VERSION}.noarch.rpm /tmp
RUN curl https://copr.fedorainfracloud.org/coprs/alsadi/dumb-init/repo/epel-7/alsadi-dumb-init-epel-7.repo -o /etc/yum.repos.d/alsadi-dumb-init-epel-7.repo && \
    yum -y group install "Development Tools" && \
    rpm -ivh /tmp/jenkins-${JENKINS_RPM_VERSION}.noarch.rpm

COPY ./contrib/jenkins/scripts /usr/local/bin
COPY ./contrib/openshift /opt/openshift
COPY ./contrib/s2i /usr/libexec/s2i

# Install latest version of GIT
WORKDIR /usr/src
RUN wget https://github.com/git/git/archive/v${GIT_VERSION}.tar.gz -O git.tar.gz && \
    tar xzf git.tar.gz
WORKDIR /usr/src/git-${GIT_VERSION}
RUN make configure && \
    ./configure --prefix=/usr/local && \
    make install
RUN git --version

RUN chmod 775 /usr/local/bin/* /usr/libexec/s2i/* && \
    /usr/local/bin/install-plugins.sh /opt/openshift/install-these-plugins.txt && \
    # need to create <plugin>.pinned files when upgrading "core" plugins like
    # credentials or subversion that are bundled with the jenkins server.
    # Currently jenkins v2 does not embed any plugins, but for reference:
    # touch /opt/openshift/plugins/credentials.jpi.pinned && \
    rmdir /var/log/jenkins && \
    mkdir /var/lib/jenkins/logs && \
    ln -sf /var/lib/jenkins/logs /var/log/jenkins && \
    chmod 664 /etc/passwd && \
    chmod -R 775 /etc/alternatives && \
    chmod -R 775 /var/lib/alternatives && \
    chmod -R 775 /usr/lib/jvm && \
    chmod 775 /usr/bin && \
    chmod 775 /usr/lib/jvm-exports && \
    chmod 775 /usr/share/man/man1 && \
    chmod 775 /var/lib/origin && \
    unlink /usr/bin/java && \
    unlink /usr/bin/jjs && \
    unlink /usr/bin/keytool && \
    unlink /usr/bin/orbd && \
    unlink /usr/bin/pack200 && \
    unlink /usr/bin/policytool && \
    unlink /usr/bin/rmid && \
    unlink /usr/bin/rmiregistry && \
    unlink /usr/bin/servertool && \
    unlink /usr/bin/tnameserv && \
    unlink /usr/bin/unpack200 && \
    unlink /usr/lib/jvm-exports/jre && \
    unlink /usr/share/man/man1/java.1.gz && \
    unlink /usr/share/man/man1/jjs.1.gz && \
    unlink /usr/share/man/man1/keytool.1.gz && \
    unlink /usr/share/man/man1/orbd.1.gz && \
    unlink /usr/share/man/man1/pack200.1.gz && \
    unlink /usr/share/man/man1/policytool.1.gz && \
    unlink /usr/share/man/man1/rmid.1.gz && \
    unlink /usr/share/man/man1/rmiregistry.1.gz && \
    unlink /usr/share/man/man1/servertool.1.gz && \
    unlink /usr/share/man/man1/tnameserv.1.gz && \
    unlink /usr/share/man/man1/unpack200.1.gz && \
    /usr/local/bin/fix-permissions /opt/openshift && \
    /usr/local/bin/fix-permissions /var/lib/jenkins && \
    /usr/local/bin/fix-permissions /var/log && \
    chown -R jenkins:jenkins /opt/openshift && \
    chown -R jenkins:jenkins /var/lib/jenkins && \
    ln /opt/openshift/release.version /tmp/release.version && \
    usermod -a -G root jenkins

RUN alternatives --auto java

VOLUME ["/var/lib/jenkins"]

USER jenkins
ENTRYPOINT ["/usr/bin/dumb-init", "--"]
CMD ["/usr/libexec/s2i/run"]
