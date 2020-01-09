FROM library/ubuntu:16.04

RUN apt-get update

RUN apt-get install -y \
    sudo tzdata vim \
	build-essential zlib1g-dev libssl-dev libreadline-dev libyaml-dev libcurl4-openssl-dev \
	libapr1-dev libaprutil1-dev apache2-utils apache2-dev  \
	imagemagick libmagick++-dev fonts-takao-pgothic \
	subversion libapache2-svn \
	git gitweb libssh2-1 libssh2-1-dev cmake libgpg-error-dev \
	libdigest-sha-perl libapache-dbi-perl libdbd-mysql-perl libauthen-simple-ldap-perl
    # mod_dav_svn mod_authz_svn.so mod_dontdothat.so epel-release  mod_perl perl-DBI perl-DBD-Pg perl-Digest-SHA

# apache2
ADD apache2/mods-available/dav_svn.conf /etc/apache2/mods-available/

# use Redmine Auth
RUN mkdir -p /etc/perl/Apache/Authn
ADD pm/Redmine.pm /etc/perl/Apache/Authn/

# repository
RUN mkdir /var/lib/svn/
RUN chown -R www-data:www-data /var/lib/svn/

# ginaliz
EXPOSE 3690
ADD entrypoint.sh /root/
ENTRYPOINT sh /root/entrypoint.sh