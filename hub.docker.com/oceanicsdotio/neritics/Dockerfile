FROM oceanicsdotio/mono-py:latest

ENV PYTHONUNBUFFERED 1

WORKDIR neritics

COPY src ./src
COPY neritics ./neritics
COPY setup.py ./setup.py
RUN pip3 install -e .

WORKDIR /