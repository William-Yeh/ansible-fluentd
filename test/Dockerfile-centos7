# Dockerfile for building image that contains software stack provisioned by Ansible.
#
# USAGE:
#   $ docker build -t fluentd .
#   $ docker run -p 24220:24220 fluentd
#
# Version  1.0
#


# pull base image
FROM williamyeh/ansible:centos7-onbuild

MAINTAINER William Yeh <william.pjyeh@gmail.com>


#
# build phase
#

ENV PLAYBOOK test.yml
RUN ansible-playbook-wrapper -vvv --extra-vars "tdagent_use_service=False"

# port for monitoring agent
EXPOSE 24220


#
# test phase
#

RUN echo "===> Installing curl for testing purpose..."  && \
    yum -y install curl


VOLUME ["/data"]
ENV    RESULT     /data/result-centos7

CMD  /etc/init.d/td-agent start  &&  sleep 10  &&  curl --retry 5 --retry-max-time 120  http://localhost:24220/api/plugins.json  > $RESULT
