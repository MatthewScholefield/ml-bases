FROM cgr.dev/chainguard/wolfi-base

COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

RUN apk update && apk add --no-cache python-3.12 openssh bash rsync findutils

ENV UV_NO_DEV=1

RUN uv venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"
ENV VIRTUAL_ENV=/opt/venv

RUN uv pip install 'tensorflow[and-cuda]'

RUN printf '#!/bin/sh\nLD_NVIDIA=$(find /opt/venv/lib/python3.12/site-packages/nvidia -type d -name lib | tr "\\n" ":")\nexport LD_LIBRARY_PATH="${LD_NVIDIA%%:}${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}"\nexec "$@"\n' > /entrypoint.sh \
    && chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
CMD ["bash"]
