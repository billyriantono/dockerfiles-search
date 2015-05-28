FROM debian

MAINTAINER Govind R


RUN apt-get -y update \
	&& apt-get -y upgrade \
	&& apt-get install build-essential -y --no-install-recommends \
	&& apt-get install wget  -y --no-install-recommends \
	&& echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots/3.12.0 main" > /etc/apt/sources.list.d/mono-xamarin.list \
    && wget -qO - http://download.mono-project.com/repo/xamarin.gpg | apt-key add - \
	&& apt-get update \
    && apt-get install mono-runtime -y --no-install-recommends \
    && apt-get install mono-complete fsharp -y \
	&& apt-get install nuget -y \
	&& apt-get install nunit -y \
    && apt-get purge wget -y \
    && apt-get autoremove -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /var/tmp/* \
    && mono --version
