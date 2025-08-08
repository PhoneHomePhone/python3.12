ARG IMAGE_BASE="ubuntu:22.04"
FROM ${IMAGE_BASE}

LABEL org.opencontainers.image.source="https://github.com/PhoneHomePhone/ai-dock-python-base"
LABEL org.opencontainers.image.description="A custom Python development environment with Python 3.12, based on the ai-dock framework."
LABEL maintainer="https://github.com/PhoneHomePhone/"

USER root
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    software-properties-common \
    ca-certificates \
    && add-apt-repository -y ppa:deadsnakes/ppa && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
    python3.12 \
    python3.12-venv \
    python3.12-dev \
    python3-pip \
    && apt-get clean && rm -rf /var/lib/apt/lists/*
RUN update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.12 1
RUN python3 -m pip install --no-cache-dir --upgrade pip
RUN python3 -m pip install --no-cache-dir --upgrade setuptools supervisor

ENV JUPYTER_VENV=$VENV_DIR/jupyter
ENV JUPYTER_VENV_PYTHON=$JUPYTER_VENV/bin/python
ENV JUPYTER_VENV_PIP=$JUPYTER_VENV/bin/pip

COPY --chown=0:1111 ./COPY_ROOT_0/ /

ARG PYTHON_VERSION="3.12"
ENV PYTHON_VERSION=${PYTHON_VERSION}

ARG PYTHON_VENV_NAME="python_312"
ENV PYTHON_VENV_NAME=${PYTHON_VENV_NAME}

ENV PYTHON_DEFAULT_VENV="jupyter"

ENV OPT_SYNC=$OPT_SYNC
ENV IMAGE_SLUG="python"

RUN set -eo pipefail && /opt/ai-dock/bin/build/layer0/init.sh | tee /var/log/build.log

CMD ["init.sh"]