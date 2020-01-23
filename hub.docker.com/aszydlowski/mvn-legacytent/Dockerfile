# Build command:
#
#     docker build --no-cache --pull --tag asukakenji/tensorflow-py36:latest .
#

FROM tensorflow/tensorflow:latest-py3

COPY TypeCheckDemo.ipynb /notebooks/

RUN apt-add-repository -y ppa:deadsnakes/ppa

RUN apt-get update

RUN apt-get install -y python3.6 python3.6-dev python3.6-venv

RUN curl --silent --show-error --location --remote-name --remote-time https://bootstrap.pypa.io/get-pip.py

RUN python3.6 -m get-pip

# Move to $HOME to avoid appearing in the notebook's file listing
RUN mv get-pip.py $HOME/

RUN python3.6 -m pip install ipykernel

RUN python3.6 -m ipykernel install

RUN python3.6 -m pip install mypy

RUN curl --silent --show-error --location --remote-name --remote-time https://gist.githubusercontent.com/knowsuchagency/f7b2203dd613756a45f816d6809f01a6/raw/c9c1b7ad9fa25a57ee1903d755d5525894ffa411/typecheck.py

# Create the profile directory
RUN ipython locate profile

RUN mv typecheck.py "$(ipython locate profile)/startup/"
