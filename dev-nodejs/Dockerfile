FROM phusion/baseimage:0.9.11
MAINTAINER Rodolfo Ripado <ggaspaio@gmail.com>

# Dev user is root
ENV HOME /root


# Utilities & dev specific stuff
# #######################################################
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get upgrade -y && \
    DEBIAN_FRONTEND=noninteractive apt-get install wget man htop git build-essential python -y

RUN echo "Europe/Paris" > /etc/timezone && \
    DEBIAN_FRONTEND=noninteractive dpkg-reconfigure tzdata

RUN update-alternatives --set editor /usr/bin/vim.basic


# PGSQL Client
#########################################################
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main" > /etc/apt/sources.list.d/pgdg.list
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
RUN sudo apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y postgresql-client libpq-dev


# NodeJS install via NVM + dev tools
#########################################################
ENV NVM_DIR /root/.nvm

RUN wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.10.0/install.sh | bash

# Enable nvm on SSH connections to container
RUN echo "[[ -s $HOME/.nvm/nvm.sh ]] && . $HOME/.nvm/nvm.sh" >> $HOME/.bashrc

# Install node and set it as default on login
RUN bash -c '. $HOME/.nvm/nvm.sh && nvm install 0.10.28'
RUN bash -c '. $HOME/.nvm/nvm.sh && nvm alias default 0.10.28'
RUN bash -c '. $HOME/.nvm/nvm.sh && npm install -g grunt-cli'

#


# Clean-ups
# #######################################################

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Use baseimage-docker's init system (default) with insecure SSH (after all, it's dev).
CMD ["/sbin/my_init", "--enable-insecure-key"]

