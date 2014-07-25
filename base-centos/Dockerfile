
FROM centos:centos6
MAINTAINER Rodolfo Ripado <ggaspaio@gmail.com>

# Set Europe/Paris localtime
RUN ln -f -s /usr/share/zoneinfo/Europe/Paris /etc/localtime

# Correct locale
# The centos Docker basebox deletes loads of executables to save space, but we need localedef
# We should problably re-remove them.
# Cf. https://github.com/dotcloud/docker/blob/master/contrib/mkimage-yum.sh
ENV LANG en_US.UTF-8
RUN yum reinstall glibc-common
RUN localedef -v -c -i en_US -f UTF-8 en_US.UTF-8


# Extra package sources & update
RUN rpm --import https://fedoraproject.org/static/0608B895.txt
RUN rpm -Uvh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm

RUN rpm --import http://dag.wieers.com/rpm/packages/RPM-GPG-KEY.dag.txt
RUN rpm -Uvh http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.3-1.el6.rf.x86_64.rpm

RUN yum upgrade -y

# Base packages
RUN yum install htop wget vim -y

# Set vim as default editor
RUN echo $'export VISUAL=\"vim\"\nexport EDITOR=\"vim\"' | tee /etc/profile.d/editor.sh

CMD ["/bin/bash"]
