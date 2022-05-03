# +-----------------------------+
# | BASE IMAGE                  |
# +-----------------------------+

FROM python:3.9

# +-----------------------------+
# | ARGS                        |
# +-----------------------------+

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# +-----------------------------+
# | ENV                         |
# +-----------------------------+

ENV DEBIAN_FRONTEND=noninteractive

# +-----------------------------+
# | FILES                       |
# +-----------------------------+

COPY requirements.txt /tmp/requirements.txt

# +-----------------------------+
# | PRE-REQUISITES/INIT PACKAGES |
# +-----------------------------+

# avoid debconf delaying package configuration, since apt-utils is not installed
RUN apt update && \
    apt install -y --no-install-recommends apt-utils dialog 2>&1

RUN apt update && \
    apt install -y build-essential

RUN apt install -y python3 \
    python3-dev \
    python3-pip \
    python3-venv \
    python3-wheel \
    python3-setuptools

# Cleanup
RUN apt-get autoremove -y && \
    apt-get clean autoclean && \
    rm -rf /var/lib/apt/lists/*

# Install base Python Packages
RUN pip3 install --upgrade pip && \
    pip3 install setuptools --upgrade && \
    pip3 install wheel && \
    pip3 install ipykernel docutils jupyter pyyaml pylint black

# Install specifig Python packages
Run pip3 install -r /tmp/requirements.txt

# re-enable dialog mode for apt-get
ENV DEBIAN_FRONTEND=dialog
