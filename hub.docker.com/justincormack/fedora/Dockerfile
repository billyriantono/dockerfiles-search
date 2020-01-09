FROM fedora

RUN dnf -y update && dnf install -y iputils which libcap

RUN capsh --print
