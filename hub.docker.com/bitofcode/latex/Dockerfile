FROM debian:10-slim

ENV LATEX_USER "latex-user"

RUN apt-get update && \
  apt-get upgrade -y && \
  apt-get install -y texlive-full git-all python3-pip python-pip && \
  useradd --create-home --shell /bin/bash ${LATEX_USER}

USER ${LATEX_USER}

WORKDIR /home/${LATEX_USER}

CMD ["/bin/bash"]
