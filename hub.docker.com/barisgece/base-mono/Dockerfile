FROM debian:stretch-slim

LABEL Baris Gece <gece.baris@gmail.com>

ENV MONO_VERSION 5.18.0.240

# Grab MONO’s APT repo GPG key -- Tianon Gravi Approach > https://ram.tianon.xyz/post/2016/12/07/docker-setup.html
RUN apt-get -qqy update \
  && apt list --upgradable \
  && apt-get install -qqy --no-install-recommends gnupg dirmngr \
  && rm -rf /var/lib/apt/lists/* \
  && export GNUPGHOME="$(mktemp -d)" \
  && gpg --batch --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF \
  && gpg --batch --export --armor 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF | tee /etc/apt/trusted.gpg.d/mono.gpg.asc > /dev/null \
  ## && gpg --batch --export 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF | tee /etc/apt/trusted.gpg.d/mono.gpg > /dev/null \
  && gpgconf --kill all \
  && rm -rf "$GNUPGHOME" \
  && apt-key list | grep Xamarin \
  && apt-get purge -qqy --auto-remove gnupg dirmngr

# Note 1 : gnupg, gnupg2 and gnupg1 is not installed on debian:stretch-slim. So,`gnupg` `dirmngr` should be installed

# Note 2 : If APT does not support .asc files in /etc/apt/trusted.gpg.d as jessie(Debian 8), you should use 
## `gpg ---batch -export 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF | sudo tee /etc/apt/trusted.gpg.d/mono.gpg > /dev/null`

# Note 3 : If install dirmngr without --no-install-recommends, gnupg will be installed automatically

# Note 4 : If you want to install deb pack from https, you should install `apt-transport-https`
## Because, https support has been moved into the apt package after version 1.5. Stretch(Debian 9) has APT v1.4.9 
## Buster new Debian Release it's still testing. It's incluede 1.8.0 - And https://packages.debian.org/sid/apt-transport-https
## Sid unstable Debian Release . It's incluede 1.8.0 https://packages.debian.org/sid/apt-transport-https

RUN echo "deb http://download.mono-project.com/repo/debian stable-stretch/snapshots/$MONO_VERSION main" | tee /etc/apt/sources.list.d/mono-official-stable.list \
  && apt-get -qqy update \
  && apt-get install -qqy mono-runtime binutils curl mono-devel ca-certificates-mono fsharp mono-vbnc nuget referenceassemblies-pcl \
&& rm -rf /var/lib/apt/lists/* /tmp/*

# MONO Packages
## The package mono-devel should be installed to compile code.
## The package mono-complete should be installed to install everything - this should cover most cases of "assembly not found" errors.
## The package mono-dbg should be installed to get debugging symbols for framework libraries - allowing you to get line numbers in stack traces.
## The package referenceassemblies-pcl should be installed for PCL compilation support - this will resolve most cases of "Framework not installed: .NETPortable" errors during software compilation.
## The package ca-certificates-mono should be installed to get SSL certificates for HTTPS connections. Install this package if you run into trouble making HTTPS connections.
## The package mono-xsp4 should be installed for running ASP.NET applications.