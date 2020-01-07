# Pull base image
FROM circleci/python:3.4.8
USER circleci

RUN \
  echo "Downloading and setting up pyenv" && \
  cd && curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash && \
  echo 'export PATH="/home/circleci/.pyenv/bin:$PATH"' >> ~/.bashrc && \
  echo 'eval "$(pyenv init -)"' >> ~/.bashrc && \
  echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc

CMD ["/bin/bash"]