FROM cgr.dev/chainguard/wolfi-base

COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

RUN apk update && apk add --no-cache python-3.12 openssh bash rsync findutils

ENV UV_NO_DEV=1

RUN uv venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"
ENV VIRTUAL_ENV=/opt/venv

RUN uv pip install 'tensorflow[and-cuda]'

RUN NVIDIA_LIBS=$(find /opt/venv/lib/python3.12/site-packages/nvidia -type d -name lib | paste -sd ':' -) \
    && printf 'export PATH="/opt/venv/bin:$PATH"\nexport VIRTUAL_ENV=/opt/venv\nexport LD_LIBRARY_PATH="%s${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}"\n' "$NVIDIA_LIBS" \
       > /etc/profile.d/venv.sh

ENV BASH_ENV=/etc/profile.d/venv.sh

CMD ["bash"]
