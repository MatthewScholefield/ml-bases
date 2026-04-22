FROM cgr.dev/chainguard/wolfi-base

RUN apk update && apk add --no-cache python-3.12 py3.12-pip openssh bash

WORKDIR /app

RUN adduser -D -u 1000 appuser
USER appuser

RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir 'tensorflow[and-cuda]'
