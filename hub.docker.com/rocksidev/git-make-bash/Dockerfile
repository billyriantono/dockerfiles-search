FROM golang:1.13.4

RUN apt-get update && apt-get install -y curl make python3-dev python3-pip libffi-dev gcc libc-dev
RUN if [ ! -e /usr/bin/python ]; then ln -sf /usr/bin/python3 /usr/bin/python ; fi && if [ ! -e /usr/bin/pip ]; then ln -s /usr/bin/pip3 /usr/bin/pip ; fi

RUN useradd -ms /bin/bash devci

USER devci
WORKDIR /home/devci

RUN pip3 install pysftp==0.2.9
RUN mkdir -p "$HOME/.ssh" && echo "github.com ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAq2A7hRGmdnm9tUDbO9IDSwBK6TbQa+PXYPCPy6rbTrTtw7PHkccKrpp0yVhp5HdEIcKr6pLlVDBfOLX9QUsyCOV0wzfjIJNlGEYsdlLJizHhbn2mUjvSAHQqZETYP81eFzLQNnPHt4EVVUh7VfDESU84KezmD5QlWpXLmvU31/yMf+Se8xhHTvKSCZIFImWwoG6mbUoWf9nzpIoaSjB+weqqUUmpaaasXVal72J+UX2B+2RPW3RcT0eOzQgqlJL3RKrTJvdsjE3JEAvGq3lGHSZXy28G3skua2SmVi/w4yCE6gbODqnTWlg7+wC604ydGXA8VJiS5ap43JXiUFFAaQ==" > "$HOME/.ssh/known_hosts"

COPY ./deploy.py /usr/local/bin/deploy.py
COPY ./make_report_time.sh /usr/local/bin/make_report_time.sh
