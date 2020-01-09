FROM ocaml/ocaml:ubuntu-16.04
LABEL distro_style="apt" distro="ubuntu" distro_long="ubuntu-16.04" arch="x86_64" ocaml_version="4.02.3" opam_version="1.2" operatingsystem="linux"
#RUN bash -c "echo yes | add-apt-repository ppa:avsm/ocaml42+opam12"
RUN apt-get -y update
RUN DEBIAN_FRONTEND=noninteractive apt-get -y upgrade && \
    DEBIAN_FRONTEND=noninteractive apt-get -y install aspcud git \
                    time libsqlite3-dev \
                    libev-dev libgmp-dev emacs vim tmux \
                    libpq-dev wget zlib1g-dev screen nfs-common \
                    lilypond ispell
RUN wget https://github.com/ocaml/opam/releases/download/1.2.2/opam-1.2.2-x86_64-Linux
RUN cp opam-1.2.2-x86_64-Linux /usr/bin/opam
RUN chmod a+rx /usr/bin/opam
#
# RUN git clone -b 1.2 git://github.com/ocaml/opam /tmp/opam && \
#     sh -c "cd /tmp/opam && make cold && make install && rm -rf /tmp/opam"
RUN echo 'opam ALL=(ALL:ALL) NOPASSWD:ALL' > /etc/sudoers.d/opam && \
    chmod 440 /etc/sudoers.d/opam && \
    chown root:root /etc/sudoers.d/opam && \
    adduser --disabled-password --gecos '' opam && \
    passwd -l opam && \
    chown -R opam:opam /home/opam
USER opam
ENV HOME /home/opam
WORKDIR /home/opam

## RUN sudo mkdir /opamroot/
## RUN sudo chown opam:opam /opamroot/
## ENV OPAMROOT /opamroot/
## ENV OPAMYES 1
## RUN opam init --yes --comp=4.02.3
## RUN opam config setup -a
## RUN bash -c "opam install -y sqlite3 tls conf-libev"
## RUN bash -c "opam pin --yes add ketrew https://github.com/hammerlab/ketrew.git"
## RUN opam install --yes tlstunnel
## RUN opam pin --yes add solvuu-build https://github.com/solvuu/solvuu-build.git
## RUN opam pin --yes add coclobas https://github.com/hammerlab/coclobas.git

