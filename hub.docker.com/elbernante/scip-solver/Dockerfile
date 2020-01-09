FROM elbernante/python-scip:3.6.6-alpine3.8-6.0.0

# Install dependencies
COPY Pipfile Pipfile.lock /app/

WORKDIR /app

RUN apk update && \
    apk add --no-cache --virtual .build-deps python3-dev g++ && \
    ln -s /usr/include/locale.h /usr/include/xlocale.h && \
    pip install pipenv && \
    pipenv install --system --deploy && \
    apk del .build-deps

COPY src /app/src/

EXPOSE 50051

CMD ["python", "src"]