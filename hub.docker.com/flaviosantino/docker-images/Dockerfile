FROM opensuse:13.2

MAINTAINER Flavio Pereira "flaviosantino@gmail.com"

# make sure the repositories are up to date
RUN zypper --non-interactive --gpg-auto-import-keys ref

RUN zypper in -y patterns-openSUSE-base
RUN zypper in -y openssh
