FROM startx/sv-php:latest

ENV SX_VERSION="latest" \
    SX_TYPE="runner" \
    SX_SERVICE="php" \
    SX_ID="startx/runner-php" \
    SX_NAME="Startx Apache-PHP gitlab runner image (fedora rawhide)" \
    SX_SUMMARY="Startx apache-php gitlab runner based on fedora rawhide"

LABEL name="$SX_ID" \
    summary="$SX_SUMMARY" \
    description="$SX_SUMMARY. Use for building application based on php using gitlab CI runners." \
    version="$SX_VERSION" \
    release="$SX_VERSION" \
    io.k8s.description="$SX_SUMMARY" \
    io.k8s.display-name="$SX_ID" \
    io.openshift.min-memory="300Mi" \
    io.openshift.min-cpu="2000m" \
    fr.startx.component="$SX_ID:$SX_VERSION"

USER root
RUN dnf install -yq yum-utils dnf-plugin-system-upgrade && \
    dnf upgrade -yq --refresh && \
    dnf install -yq --nogpgcheck \
    make \
    bubblewrap \
    rsync \
    openssh-clients \
    sshpass && \
    package-cleanup --problems && \
    package-cleanup --orphans && \
    dnf remove -yq --skip-broken dnf-plugin-system-upgrade yum-utils yum && \
    dnf clean all --enablerepo=\*

USER 1001

CMD [ "/bin/sx-php" , "usage" ]
