FROM phusion/baseimage:0.9.11
MAINTAINER Rodolfo Ripado <ggaspaio@gmail.com>

# Dev user is root
ENV HOME /root


# Utilities & dev specific stuff
# #######################################################
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get upgrade -y && \
    DEBIAN_FRONTEND=noninteractive apt-get install wget man htop -y

RUN echo "Europe/Paris" > /etc/timezone && \
    DEBIAN_FRONTEND=noninteractive dpkg-reconfigure tzdata

RUN update-alternatives --set editor /usr/bin/vim.basic


# Clean-ups
# #######################################################

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Use baseimage-docker's init system (default) with insecure SSH (after all, it's dev).
CMD ["/sbin/my_init", "--enable-insecure-key"]

