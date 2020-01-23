
# openshift-vault
FROM openshift/base-centos7

# TODO: Put the maintainer name in the image metadata
# MAINTAINER Your Name <your@email.com>

# TODO: Rename the builder environment variable to inform users about application you provide them
# ENV BUILDER_VERSION 1.0

# TODO: Set labels used in OpenShift to describe the builder image
#LABEL io.k8s.description="Platform for building xyz" \
#      io.k8s.display-name="builder x.y.z" \
#      io.openshift.expose-services="8080:http" \
#      io.openshift.tags="builder,x.y.z,etc."

# TODO: Install required packages here:
RUN yum install -y unzip && yum clean all -y

# TODO (optional): Copy the builder files into /opt/app-root
# COPY ./<builder_folder>/ /opt/app-root/
RUN curl https://releases.hashicorp.com/vault/0.6.1/vault_0.6.1_linux_amd64.zip > vault.zip && unzip vault.zip && chmod +x vault && rm vault.zip


# TODO: Copy the S2I scripts to /usr/libexec/s2i, since openshift/base-centos7 image sets io.openshift.s2i.scripts-url label that way, or update that label
# COPY ./.s2i/bin/ /usr/libexec/s2i

# TODO: Drop the root user and make the content of /opt/app-root owned by user 1001
RUN mkdir /opt/vault
RUN chown -R 1001:1001 /opt/vault

# This default user is created in the openshift/base-centos7 image
USER 1001

# TODO: Set the default port for applications built using this image
EXPOSE 8200

ENV VAULT_DEV_LISTEN_ADDRESS "0.0.0.0:8200"

# TODO: Set the default CMD for the image
CMD ["./vault", "server", "--dev"]
