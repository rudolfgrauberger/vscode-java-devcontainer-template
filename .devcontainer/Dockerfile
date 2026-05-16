FROM bellsoft/liberica-openjdk-debian:25.0.3

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=${USER_UID}

RUN apt-get update \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        git \
        jq \
        unzip \
    && groupadd --gid ${USER_GID} ${USERNAME} \
    && useradd --uid ${USER_UID} --gid ${USER_GID} -m ${USERNAME} \
    && mkdir -p /home/${USERNAME}/.m2 \
    && chown -R ${USERNAME}:${USERNAME} /home/${USERNAME} \
    && rm -rf /var/lib/apt/lists/*

USER ${USERNAME}
WORKDIR /workspaces
