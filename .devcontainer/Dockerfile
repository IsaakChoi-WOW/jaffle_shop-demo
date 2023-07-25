## Start with base image of alpine linux with git installed
FROM mcr.microsoft.com/devcontainers/base:bullseye

## ISSUES ## 
## May be causing crashes on my computer - Mac M2 Pro
# `add-apt-repository universe` command
# `DEBIAN_FRONTEND=noninteractive` flag
## Look at: https://github.com/microsoft/vscode-remote-release/issues/7450 for crashes

# ## FOR SOME REASON CRASHES ON MY COMPUTER - Mac M2 Pro - Set install parameters
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && yes | unminimize 2>&1 
ENV LANG="C.UTF-8"

## Install packages
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y --no-install-recommends \
        xz-utils \
        python-pip-whl \
        python3-pip

## Default to bash shell (other shells available at /usr/bin/fish and /usr/bin/zsh)
ENV SHELL=/bin/bash \
    DOCKER_BUILDKIT=1

## Install and setup fish
RUN apt-get install -yq fish
RUN FISH_PROMPT="function fish_prompt\n    set_color green\n    echo -n (whoami)\n    set_color normal\n    echo -n \":\"\n    set_color blue\n    echo -n (pwd)\n    set_color normal\n    echo -n \"> \"\nend\n"
RUN printf "$FISH_PROMPT" >> /etc/fish/functions/fish_prompt.fish
RUN printf "if type code-insiders > /dev/null 2>&1; and not type code > /dev/null 2>&1\n  alias code=code-insiders\nend" >> /etc/fish/conf.d/code_alias.fish

## Other cleanup
# RUN rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get upgrade -y
# RUN rm -rf /var/lib/apt/lists/*

## Remove scripts now that we're done with them
RUN apt-get clean -y && rm -rf /tmp/scripts

## Expose ports
# EXPOSE is not required for devcontainers. See 'devcontainer.json'

## Run
# CMD is not required for devcontainers. 
# Note to me: See what is used by default in this case 'docker container list'

