FROM python

RUN apt update
WORKDIR /ansible-playbook-grapher
ADD . .
RUN pip install -r requirements.txt
RUN apt install -y graphviz
RUN pip install cairosvg
RUN pip install ansible
RUN pip install packaging
RUN pip install ansible-playbook-grapher
#RUN make build
# git checkout fix/ansible28CLI
COPY generate-graph.sh /usr/local/bin/generate-graph
WORKDIR /work

