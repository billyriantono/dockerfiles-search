FROM michilu/fedora-zero
# Switch to dnf.
RUN yum install --setopt=rawhide.skip_if_unavailable=true --quiet -y dnf && dnf clean all
