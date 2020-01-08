FROM barisgece/jenkins-jnlp-slave:latest

LABEL Baris Gece <gece.baris@gmail.com>

USER root

ENV MONO_VERSION 5.18.0.240

# Grab MONO’s APT repo GPG key -- Tianon Gravi Approach > https://ram.tianon.xyz/post/2016/12/07/docker-setup.html
RUN apt-get -qqy update \
  && apt list --upgradable \
  && export GNUPGHOME="$(mktemp -d)" \
  && gpg --batch --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF \
  && gpg --batch --export --armor 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF | tee /etc/apt/trusted.gpg.d/mono.gpg.asc > /dev/null \
  ## && gpg --batch --export 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF | tee /etc/apt/trusted.gpg.d/mono.gpg > /dev/null \
  && gpgconf --kill all \
  && rm -rf "$GNUPGHOME" \
  && apt-key list | grep Xamarin 

# Note 2 : If APT does not support .asc files in /etc/apt/trusted.gpg.d as jessie(Debian 8), you should use 
## `gpg ---batch -export 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF | sudo tee /etc/apt/trusted.gpg.d/mono.gpg > /dev/null`

RUN echo "deb http://download.mono-project.com/repo/debian stable-stretch/snapshots/$MONO_VERSION main" | tee /etc/apt/sources.list.d/mono-official-stable.list \
  && apt-get -qqy update \
  && apt-get install -qqy mono-runtime binutils curl mono-devel ca-certificates-mono fsharp mono-vbnc nuget referenceassemblies-pcl \
&& rm -rf /var/lib/apt/lists/* /tmp/*

USER jenkins

ENTRYPOINT [ "jenkins-slave" ]

# MONO Packages
## The package mono-devel should be installed to compile code.
## The package mono-complete should be installed to install everything - this should cover most cases of "assembly not found" errors.
## The package mono-dbg should be installed to get debugging symbols for framework libraries - allowing you to get line numbers in stack traces.
## The package referenceassemblies-pcl should be installed for PCL compilation support - this will resolve most cases of "Framework not installed: .NETPortable" errors during software compilation.
## The package ca-certificates-mono should be installed to get SSL certificates for HTTPS connections. Install this package if you run into trouble making HTTPS connections.
## The package mono-xsp4 should be installed for running ASP.NET applications.