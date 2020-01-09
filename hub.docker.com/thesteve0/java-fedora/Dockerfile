FROM fedora:latest

#Update and clean all
RUN dnf update -y && dnf install -y java-1.8.0-openjdk jai-imageio-core wget unzip && dnf -y clean all
#RUN dnf install -y java-1.8.0-openjdk wget unzip && dnf -y clean all

CMD bash
