FROM debian:jessie

RUN apt-get update \
        && apt-get install -y curl \
        && rm -rf /var/lib/apt/lists/*

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF

RUN echo "deb http://download.mono-project.com/repo/debian wheezy main" | tee /etc/apt/sources.list.d/mono-xamarin.list \
    echo "deb http://download.mono-project.com/repo/debian wheezy-libjpeg62-compat main" | tee -a /etc/apt/sources.list.d/mono-xamarin.list \
        && apt-get update \
        && apt-get install -y mono-runtime ca-certificates-mono python python-pip \
        && rm -rf /var/lib/apt/lists/*

RUN apt-get update \
        && apt-get install -y libgfortran3 libgomp1 nco grads \
        && rm -rf /var/lib/apt/lists/*

RUN pip install awscli \
        && rm -rf /tmp/pip*

ADD files/usr/local /usr/local