## Start with base image of alpine linux with git installed
FROM mcr.microsoft.com/devcontainers/base:bullseye


## ISSUES ## 
# `add-apt-repository universe` command may be causing crashes on my computer - Mac M2 Pro
# May be helpful: https://github.com/microsoft/vscode-remote-release/issues/7450
# `yes | unminimize 2>&1` 'unminimize' not found (and not present in sbin directory)


### Setup ###

## General
RUN apt-get update && apt-get upgrade -y
RUN export DEBIAN_FRONTEND=noninteractive
ENV LANG="C.UTF-8"

## Unminimise
# RUN yes | unminimize 2>&1 

## Default to bash shell (other shells available at /usr/bin/fish and /usr/bin/zsh)
ENV SHELL=/bin/bash \
    DOCKER_BUILDKIT=1


### Install packages ###

## Install basic
RUN apt-get install -y --no-install-recommends \
        xz-utils                 

## Install Pip
RUN apt-get install -y --no-install-recommends \
        python-pip-whl            \
        python3-pip               

## Install PostgreSQL
RUN apt-get -y install gnupg2
RUN curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc|sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" | tee  /etc/apt/sources.list.d/pgdg.list
RUN apt -y install postgresql-13 postgresql-client-13
#
RUN sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
RUN apt-get update
RUN apt-get install -y --no-install-recommends \
        postgresql                \
        postgresql-client         \
        libpq-dev                 \
        postgresql-server-dev-12 

## Install dbt
RUN pip install   \
    dbt-core      \
    dbt-postgres  \
    dbt-redshift  \
    dbt-snowflake \
    dbt-bigquery  \
    dbt-trino     
    

# ## Verify expected build and debug tools are present
# RUN apt-get update \
#     && apt-get -y install build-essential cmake cppcheck valgrind clang lldb llvm gdb python3-dev \
#     ## Install tools and shells not in common script
#     && apt-get install -yq vim vim-doc xtail software-properties-common libsecret-1-dev \
#     ## Install additional tools (useful for 'puppeteer' project)
#     && apt-get install -y --no-install-recommends libnss3 libnspr4 libatk-bridge2.0-0 libatk1.0-0 libx11-6 libpangocairo-1.0-0 \
#                                                   libx11-xcb1 libcups2 libxcomposite1 libxdamage1 libxfixes3 libpango-1.0-0 libgbm1 libgtk-3-0 \
#     ## Clean up
#     && apt-get autoremove -y && apt-get clean -y \
#     ## Move first run notice to right spot
#     && mkdir -p "/usr/local/etc/vscode-dev-containers/"

## Install and setup fish
RUN apt-get install -yq fish
RUN FISH_PROMPT="function fish_prompt\n    set_color green\n    echo -n (whoami)\n    set_color normal\n    echo -n \":\"\n    set_color blue\n    echo -n (pwd)\n    set_color normal\n    echo -n \"> \"\nend\n"
RUN printf "$FISH_PROMPT" >> /etc/fish/functions/fish_prompt.fish
RUN printf "if type code-insiders > /dev/null 2>&1; and not type code > /dev/null 2>&1\n  alias code=code-insiders\nend" >> /etc/fish/conf.d/code_alias.fish

# ## Install pgAdmin4
# RUN curl https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo apt-key add
# RUN sh -c 'echo "deb https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'
# RUN apt install pgadmin4-web 

# # Install the public key for the repository (if not done previously):
# RUN curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub | gpg --dearmor -o /usr/share/keyrings/packages-pgadmin-org.gpg
# RUN curl https://www.pgadmin.org/static/packages_pgadmin_org.pub | apt-key add
# # Create the repository configuration file:
# RUN sh -c 'echo "deb [signed-by=/usr/share/keyrings/packages-pgadmin-org.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'
# RUN sh -c 'echo "deb https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'
# # Install for web mode only
# RUN apt install pgadmin4-web 

# Configure the webserver, if you installed pgadmin4-web:
# RUN /usr/pgadmin4/bin/setup-web.sh


### Other cleanup ###

## Clean some stuff? and update all packages to latest version
# RUN rm -rf /var/lib/apt/lists/*
# RUN apt-get update && apt-get upgrade -y
# RUN rm -rf /var/lib/apt/lists/*

## Remove scripts now that we're done with them
RUN apt-get clean -y && rm -rf /tmp/scripts


### Expose ports ###
# EXPOSE is not required for devcontainers. See 'devcontainer.json'


### Run ###
# CMD is not required for devcontainers. 
# Note to me: See what is used by default in this case 'docker container list'

