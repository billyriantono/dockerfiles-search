FROM python:3
RUN useradd -m nvchecker
USER nvchecker
ENV PATH="/home/nvchecker/.local/bin:${PATH}"
WORKDIR /home/nvchecker
RUN pip3 install --user nvchecker==1.4.4
RUN mkdir -p /home/nvchecker/data

FROM python:3-slim
RUN useradd nvchecker
USER nvchecker
ENV PATH="/home/nvchecker/.local/bin:${PATH}"
COPY --from=0 --chown=nvchecker:nvchecker /home/nvchecker /home/nvchecker
WORKDIR /home/nvchecker/data
