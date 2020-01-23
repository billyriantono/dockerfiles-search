FROM centos
RUN yum -y install cronie
CMD ["crond", "-n", "-p", "-x", "sch,proc,load"]
