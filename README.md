# Docker Image Packaging for RHEL

<img src="/alvistack.svg" width="75" alt="AlviStack">

[![GitLab pipeline status](https://img.shields.io/gitlab/pipeline/alvistack/docker-rhel/master)](https://gitlab.com/alvistack/docker-rhel/-/pipelines)
[![GitHub release](https://img.shields.io/github/release/alvistack/docker-rhel.svg)](https://github.com/alvistack/docker-rhel/releases)
[![GitHub license](https://img.shields.io/github/license/alvistack/docker-rhel.svg)](https://github.com/alvistack/docker-rhel/blob/master/LICENSE)
[![Docker Pulls](https://img.shields.io/docker/pulls/alvistack/rhel-8.svg)](https://hub.docker.com/r/alvistack/rhel-8)

Red Hat Enterprise Linux (often abbreviated to RHEL) is a Linux distribution developed by Red Hat for the commercial market. Red Hat Enterprise Linux is released in server versions for x86-64, Power ISA, ARM64, and IBM Z and a desktop version for x86-64. All of Red Hat's official support and training, together with the Red Hat Certification Program, focuses on the Red Hat Enterprise Linux platform.

Learn more about RHEL: <https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux>

## Supported Tags and Respective Packer Template Links

  - [`alvistack/rhel-8`](https://hub.docker.com/r/alvistack/rhel-8)
      - [`packer/docker-8/packer.json`](https://github.com/alvistack/docker-rhel/blob/master/packer/docker-8/packer.json)
  - [`alvistack/rhel-7`](https://hub.docker.com/r/alvistack/rhel-7)
      - [`packer/docker-7/packer.json`](https://github.com/alvistack/docker-rhel/blob/master/packer/docker-7/packer.json)

## Overview

This Docker container makes it easy to get an instance of SSHD up and running with RHEL.

Based on [Official RHEL Docker Image](https://access.redhat.com/articles/4238681) with some minor hack:

  - Packaging by Packer Docker builder and Ansible provisioner in single layer
  - Handle `ENTRYPOINT` with [catatonit](https://github.com/openSUSE/catatonit)
  - Handle `CMD` with SSHD

### Quick Start

Start SSHD:

    # Pull latest image
    docker pull alvistack/rhel-8
    
    # Run as detach
    docker run \
        -itd \
        --name rhel \
        --publish 2222:22 \
        alvistack/rhel-8

**Success**. SSHD is now available on port `2222`.

Because this container **DIDN'T** handle the generation of root password, so you should set it up manually with `pwgen` by:

    # Generate password with pwgen
    PASSWORD=$(docker exec -i centos pwgen -cnyB1); echo $PASSWORD
    
    # Inject the generated password
    echo "root:$PASSWORD" | docker exec -i centos chpasswd

Alternatively, you could inject your own SSH public key into container's authorized\_keys by:

    # Inject your own SSH public key
    (docker exec -i centos sh -c "cat >> /root/.ssh/authorized_keys") < ~/.ssh/id_rsa.pub

Now you could SSH to it as normal:

    ssh root@localhost -p 2222

## Versioning

### `YYYYMMDD.Y.Z`

Release tags could be find from [GitHub Release](https://github.com/alvistack/docker-rhel/releases) of this repository. Thus using these tags will ensure you are running the most up to date stable version of this image.

### `YYYYMMDD.0.0`

Version tags ended with `.0.0` are rolling release rebuild by [GitLab pipeline](https://gitlab.com/alvistack/docker-rhel/-/pipelines) in weekly basis. Thus using these tags will ensure you are running the latest packages provided by the base image project.

## License

  - Code released under [Apache License 2.0](LICENSE)
  - Docs released under [CC BY 4.0](http://creativecommons.org/licenses/by/4.0/)

## Author Information

  - Wong Hoi Sing Edison
      - <https://twitter.com/hswong3i>
      - <https://github.com/hswong3i>
