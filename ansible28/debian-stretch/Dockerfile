FROM debian:stretch

# Labels.
LABEL maintainer="will@willhallonline.co.uk" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.build-date=$BUILD_DATE \
    org.label-schema.vcs-ref=$VCS_REF \
    org.label-schema.name="willhallonline/ansible" \
    org.label-schema.description="Ansible inside Docker" \
    org.label-schema.url="https://github.com/willhallonline/docker-ansible" \
    org.label-schema.vcs-url="https://github.com/willhallonline/docker-ansible" \
    org.label-schema.vendor="Will Hall Online" \
    org.label-schema.docker.cmd="docker run --rm -it -v $(pwd):/ansible -v ~/.ssh/id_rsa:/root/id_rsa willhallonline/ansible:2.7-ubuntu-16.04"

  
RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
    apt-get install -y python-pip sshpass openssh-client && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean
    
RUN python2 -m pip install --upgrade pip cffi && \
    pip install ansible && \
    pip install mitogen ansible-lint && \
    pip install --upgrade pywinrm

RUN mkdir -p /etc/ansible && \
    echo 'localhost' > /etc/ansible/hosts

CMD [ "ansible-playbook", "--version" ]