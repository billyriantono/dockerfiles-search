FROM ubuntu:latest

# define environment variable(s)
ENV SHELLDIR /shellinabox

# add our desired username and set the password
RUN useradd -m -g users -G sudo username
RUN echo "username:password" | chpasswd

# install prerequisite packages
RUN apt-get update && apt-get install -y git libssl-dev libpam0g-dev zlib1g-dev dh-autoreconf

# clone forked shellinabox with no-ssl fix
RUN git clone https://github.com/stphnsmpsn/shellinabox.git

#set workind firectory and build/install shellinabox
WORKDIR $SHELLDIR
RUN autoreconf -i && ./configure --disable-ssl && make install

# run shellinabox on container creation
CMD shellinaboxd -s /:LOGIN
