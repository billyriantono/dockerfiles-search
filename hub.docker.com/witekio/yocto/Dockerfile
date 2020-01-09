FROM debian:latest

# Change user to root
USER root

# Add contrib and non-free repository to apt/source.list for repo
RUN sed -i 's/main/main contrib non-free/g' /etc/apt/sources.list

# Update the container
RUN apt update && apt-get upgrade -y

# Install needed package
RUN apt update && apt-get -y install \
	    asciidoc autoconf automake bc bison build-essential chrpath \
	    coreutils cpio cscope curl cvs desktop-file-utils diffstat \
	    docbook-utils dosfstools e2fslibs-dev exuberant-ctags g++ gawk \
	    gcc gcc-multilib git-core g++-multilib groff help2man \
	    iputils-ping libarchive-dev libattr1-dev libcap-dev libfuse-dev \
	    libgirepository1.0-dev libgl1-mesa-dev libglu1-mesa-dev \
	    libgpgme11-dev liblzma-dev libsdl1.2-dev libsoup2.4-dev libtool \
	    locales locales-all lzop make mercurial nano ncurses-term \
	    python3 python3-gi python-pysqlite2 repo screen sed socat sshpass \ 
	    subversion sudo texi2html texinfo u-boot-tools unzip vim wget \
	    xterm zsh

# Set the correct locales for Yocto build
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && locale-gen
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Set the new user parameter.
ARG user=jenkins
ARG group=jenkins
ARG uid=1000
ARG gid=1000
RUN groupadd -g ${gid} ${group}
RUN useradd -c "Jenkins user" -d /home/${user} -u ${uid} -g ${gid} -m ${user}

# Set HOME env variable
ENV HOME /home/${user}

# Set minimal gitconfig so CI jobs can be done without issue.
RUN git config --global user.name "${user}"
RUN git config --global user.email "${user}"
RUN git config --global color.ui false

# Create .ssh folder
RUN mkdir ${HOME}/.ssh
RUN chmod 700 ${HOME}/.ssh

# Add usefull knowns hosts for ssh
RUN ssh-keyscan bitbucket.org >> ${HOME}/.ssh/known_hosts
RUN ssh-keyscan github.com >> ${HOME}/.ssh/known_hosts
RUN ssh-keyscan gitlab.com >> ${HOME}/.ssh/known_hosts

# Change the right of the known hosts file.
RUN chmod 600 ${HOME}/.ssh/known_hosts

# Change the owner of .ssh folder
RUN chown -R ${user}:${group} ${HOME}/.ssh

# Set workdir
WORKDIR ${HOME}

# Good practice, switch back to user.
USER ${user}
