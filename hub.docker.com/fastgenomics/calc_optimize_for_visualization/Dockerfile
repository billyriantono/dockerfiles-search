FROM fastgenomics/scanpy:1.3.1-p36-v3 as base

# Install dependencies
COPY requirements.txt /
RUN apk add --update --no-cache git && \
        pip3 install --no-cache-dir -r /requirements.txt

# Copy the required app files and the app itself into /app/
COPY manifest.json LICENSE LICENSE-THIRD-PARTY /app/

COPY calc_optimize_for_visualization /app/calc_optimize_for_visualization

WORKDIR /app/
ENV PYTHONPATH /app/

# run the tests
FROM base as test
ENV PYTHONDONTWRITEBYTECODE=1
COPY tests /tests
RUN pytest -p no:warnings /tests

FROM base as final
CMD python3 -m calc_optimize_for_visualization
