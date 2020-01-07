FROM ubuntu:14.04

# much of this was gleaned from https://github.com/lxc/lxc/blob/lxc-0.8.0/templates/lxc-ubuntu.in
# and then heavily modified and hacked like crazy

# we're going to want this bad boy installed so we can connect :)
RUN apt-get update && apt-get install -y ssh

ADD init-fake.conf /etc/init/fake-container-events.conf

# undo some leet hax of the base image
RUN rm /usr/sbin/policy-rc.d; \
	rm /sbin/initctl; dpkg-divert --rename --remove /sbin/initctl

# generate a nice UTF-8 locale for our use
RUN locale-gen en_US.UTF-8 && update-locale LANG=en_US.UTF-8

# remove some pointless services
RUN /usr/sbin/update-rc.d -f ondemand remove; \
	for f in \
		/etc/init/u*.conf \
		/etc/init/mounted-dev.conf \
		/etc/init/mounted-proc.conf \
		/etc/init/mounted-run.conf \
		/etc/init/mounted-tmp.conf \
		/etc/init/mounted-var.conf \
		/etc/init/hostname.conf \
		/etc/init/networking.conf \
		/etc/init/tty*.conf \
		/etc/init/plymouth*.conf \
		/etc/init/hwclock*.conf \
		/etc/init/module*.conf\
	; do \
		dpkg-divert --local --rename --add "$f"; \
	done; \
	echo '# /lib/init/fstab: cleared out for bare-bones Docker' > /lib/init/fstab

# small fix for SSH in 13.10 (that's harmless everywhere else)
RUN sed -ri 's/^session\s+required\s+pam_loginuid.so$/session optional pam_loginuid.so/' /etc/pam.d/sshd

RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config

# let Upstart know it's in a container
ENV container docker

# set a cheap, simple password for great convenience
RUN echo 'root:docker.io' | chpasswd

RUN echo "deb http://cran.rstudio.com/bin/linux/ubuntu trusty/  " >> /etc/apt/sources.list
RUN echo "deb http://ppa.launchpad.net/ubuntugis/ubuntugis-unstable/ubuntu trusty main " >> /etc/apt/sources.list
RUN echo "deb-src http://ppa.launchpad.net/ubuntugis/ubuntugis-unstable/ubuntu trusty main " >> /etc/apt/sources.list

RUN echo "deb http://ppa.launchpad.net/grass/grass-devel/ubuntu trusty main " >> /etc/apt/sources.list
RUN echo "deb-src http://ppa.launchpad.net/grass/grass-devel/ubuntu trusty main " >> /etc/apt/sources.list

RUN apt-get update
RUN apt-get upgrade -y

RUN apt-get install -y --force-yes build-essential language-pack-en* curl iputils-ping fuse libfuse-dev libfuse2 git mc sshfs python-setuptools python-dev libpython-dev python-pip software-properties-common python-numpy libgdal-dev python-gdal gdal-bin libproj0 libproj-dev python-pyproj libgeos-* nano wget git dialog libgdal1-dev  libgdal1h grass-core python-matplotlib python-pandas python-sympy python-scipy python-nose libblas-dev liblapack-dev gfortran ipython ipython-notebook #libgdal1-1.10.1-grass

RUN pip install scikit-learn

RUN apt-get install -y --force-yes default-jre-headless default-jre 

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9 

RUN apt-get install -y --force-yes flex firefox openssh-server bison libtiff4-dev mesa-common-dev libglu-dev  libfftw3-* libcairo2-dev python-gtk2 python-gtk2-dbg python-gtk2-dev python-wxgtk* grass70-* r-base r-base-dev r-cran-xml libapparmor1 gdebi-core xserver-xorg xdm xterm gedit-plugins

RUN sed -i 's/DisplayManager.requestPort/!DisplayManager.requestPort/g' /etc/X11/xdm/xdm-config
RUN sed -i '/#any host/c\*' /etc/X11/xdm/Xaccess

RUN apt-get update && apt-get install -y --force-yes -q \
    make \
    gcc \
    zlib1g-dev \
    python \
    python-sphinx \
    python3-sphinx \
    libzmq3-dev \
    sqlite3 \
    libsqlite3-dev \
    pandoc \
    libcurl4-openssl-dev \
    nodejs \
    nodejs-legacy


RUN apt-get update
RUN apt-get upgrade -y

RUN apt-get install -y --force-yes software-properties-common
RUN apt-get update &&
RUN apt-get install -y --force-yes vnc4server vncviewer pgadmin3 postgis

RUN pip install rpy2

RUN useradd -m javier
RUN echo -e "docker.io\ndocker.io\n" | passwd javier
RUN usermod -a -G fuse javier
RUN usermod -s /bin/bash javier
RUN adduser majavie sudo

RUN apt-add-repository -y ppa:ubuntu-mate-dev/ppa
RUN apt-add-repository -y ppa:ubuntu-mate-dev/trusty-mate
RUN apt-get update && apt-get upgrade
RUN apt-get install -y --force-yes --no-install-recommends ubuntu-mate-core ubuntu-mate-desktop

RUN Rscript -e "install.packages('XML', type = 'source');install.packages(c('devtools','png','rgdal','raster','yaml','base64enc'))"

# we can has SSH
EXPOSE 22

# pepare for takeoff
CMD ["/sbin/init"]
