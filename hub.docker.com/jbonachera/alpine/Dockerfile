FROM alpine
RUN apk -U add py3-jinja2 bash
COPY render.py /usr/bin/render.py
COPY fork_proxy.sh /usr/bin/fork_proxy.sh
ENTRYPOINT ["/bin/bash"]
