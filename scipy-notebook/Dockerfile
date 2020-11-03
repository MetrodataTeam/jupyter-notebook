ARG BASE_IMAGE=jupyter/scipy-notebook:latest

FROM ${BASE_IMAGE}

ARG REQUIREMENTS=scipy.txt
ARG INSTALL_TOOLS=true

ENV JUPYTER_ENABLE_LAB=yes
ENV GRANT_SUDO=yes
ENV RESTARTABLE=yes

USER root

COPY requirements/${REQUIREMENTS} /tmp/requirements.txt

RUN test -n ${INSTALL_TOOLS} && { \
        apt-get update && \
        apt-get install -y --no-install-recommends \
            rsync neovim less htop tmux ssh netcat nethogs tree axel iputils-ping \
            postgresql-client libpq-dev libgeos-dev \
    ;}
RUN pip install --no-cache-dir -r /tmp/requirements.txt && \
    find /tmp/ /var/cache/apt /var/lib/apt/lists -mindepth 1 -maxdepth 1 -exec rm -rf {} \;
