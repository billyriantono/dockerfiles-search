FROM tomxiong/ansible:latest

RUN pip install pyvmomi

ENV ANSIBLE_HOST_KEY_CHECKING=False

CMD [ "ansible-playbook", "--version" ]
