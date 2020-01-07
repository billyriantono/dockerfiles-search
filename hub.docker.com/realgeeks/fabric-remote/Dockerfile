FROM python:2.7

RUN pip install pyyaml requests fabric_remote pyrax slackclient git+https://github.com/a2design-company/hipster

ENV FABFILE_PATH "/data/fabfile.py"
ENV HOME /root

WORKDIR /root/
RUN ["mkdir", "/.ssh"]
ADD ssh_config /root/.ssh/ssh_config
ADD start.sh /root/

CMD ["./start.sh"]

EXPOSE 1234
