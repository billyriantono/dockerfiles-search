FROM centos:latest
RUN yum install -y python3 python3-pip git-all && alternatives --set python /usr/bin/python3 && yum groupinstall 'Development Tools' -y
COPY . sqlmap-dev

ENTRYPOINT ["python","sqlmap-dev/sqlmap.py"]
CMD ["-h"]
