FROM centos:6
RUN yum install -y libgcj \
&& curl https://www.pdflabs.com/tools/pdftk-the-pdf-toolkit/pdftk-2.02-1.el6.x86_64.rpm -o pdftk-2.02-1.el6.x86_64.rpm \
&& rpm -i pdftk-2.02-1.el6.x86_64.rpm
CMD ["pdftk"]