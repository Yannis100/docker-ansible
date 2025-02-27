FROM ubuntu:16.04

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

RUN echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu xenial main" | tee /etc/apt/sources.list.d/ansible.list && \
    echo "deb-src http://ppa.launchpad.net/ansible/ansible/ubuntu xenial main" | tee -a /etc/apt/sources.list.d/ansible.list && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 7BB9C367
   
RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
    apt-get install -y ansible python-pip sshpass openssh-client && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean
    
RUN python2 -m pip install --upgrade pip pywinrm && \
    pip install mitogen ansible-lint

RUN mkdir -p /etc/ansible && \
    echo 'localhost' > /etc/ansible/hosts

CMD [ "ansible-playbook", "--version" ]