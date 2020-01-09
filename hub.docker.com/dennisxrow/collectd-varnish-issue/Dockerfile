FROM centos:7
RUN echo $'[varnishcache_varnish52]\n\
name=varnishcache_varnish52\n\
baseurl=https://packagecloud.io/varnishcache/varnish52/el/7/$basearch\n\
repo_gpgcheck=1\n\
gpgcheck=0\n\
enabled=1\n\
gpgkey=https://packagecloud.io/varnishcache/varnish52/gpgkey\n\
sslverify=1\n\
sslcacert=/etc/pki/tls/certs/ca-bundle.crt\n\
metadata_expire=300\n'\
>> /etc/yum.repos.d/varnishcache_varnish52.repo
RUN cat /etc/yum.repos.d/varnishcache_varnish52.repo
RUN yum install epel-release -y; yum install jemalloc -y; yum install -y varnish; yum clean all
RUN yum info varnish -v
RUN yum install -y collectd
RUN yum info collectd -v
RUN yum info collectd-varnish -v
RUN yum install -y collectd-varnish
