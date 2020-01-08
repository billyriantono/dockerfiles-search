# This image provides a Scala 2.11.8 environment you can use to run your Scala
# applications.
FROM centos/s2i-base-centos7

EXPOSE 8080

ENV SCALA_VERSION=2.11.8 \
    PATH=$HOME/.local/bin:/opt/scala/bin:/opt/sbt/bin:$PATH \
    LC_ALL=en_US.UTF-8 \
    LANG=en_US.UTF-8

ENV SUMMARY="Platform for building and running Scala $SCALA_VERSION applications" \
    DESCRIPTION="Scala $SCALA_VERSION available as a docker container is a base platform for \
building and running various Scala $SCALA_VERSION applications and frameworks."

LABEL summary="$SUMMARY" \
      description="$DESCRIPTION" \
      io.k8s.description="$DESCRIPTION" \
      io.k8s.display-name="Scala 2.11.8" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="builder,scala,scala2118" \
      name="elmiko/scala-2118-centos7" \
      version="2.11.8" \
      release="1" \
      maintainer="michael mccune <msm@opbstudios>"

COPY \
    sbt-0.13.13.tgz \
    scala-2.11.8.tgz \
    /tmp/artifacts/

# Copy extra files to the image.
COPY ./root/ /

RUN yum install -y java && \
    bash -x /opt/app-root/check_for_download_sbt /tmp/artifacts/sbt-0.13.13.tgz && \
    bash -x /opt/app-root/check_for_download_scala /tmp/artifacts/scala-2.11.8.tgz && \
    tar -zxf /tmp/artifacts/sbt-0.13.13.tgz -C /opt && \
    ln -s /opt/sbt-launcher-packaging-0.13.13 /opt/sbt && \
    tar -zxf /tmp/artifacts/scala-2.11.8.tgz -C /opt && \
    ln -s /opt/scala-2.11.8 /opt/scala && \
    mkdir /tmp/.ivy2 /tmp/.sbt && \
    /opt/sbt/bin/sbt

# Copy the S2I scripts from the specific language image to $STI_SCRIPTS_PATH.
COPY ./s2i/bin $STI_SCRIPTS_PATH

# - In order to drop the root user, we have to make some directories world
#   writable as OpenShift default security model is to run the container
#   under random UID.
RUN chown -R 1001:0 /opt/app-root && \
    chown -R 1001:0 /opt/sbt && \
    chown -R 1001:0 /opt/scala && \
    chmod g+rw /opt/sbt/conf && \
    chown -R 1001:0 /tmp/.ivy2 && \
    chmod g+rw /tmp/.ivy2 && \
    chown -R 1001:0 /tmp/.sbt && \
    chmod g+rw /tmp/.sbt && \
    fix-permissions /opt/app-root && \
    rpm-file-permissions

USER 1001

# Set the default CMD to print the usage of the language image.
CMD $STI_SCRIPTS_PATH/usage
