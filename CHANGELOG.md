# Docker Image Packaging for RHEL

## YYYYMMDD.Y.Z - TBC

### Major Changes

  - Upgrade minimal Ansible community package support to 4.1.0

## 20210602.1.1 - 2021-06-02

### Major Changes

  - Initialize with `verify.yml` with first start
  - Support RHEL 8.4
  - Upgrade minimal Ansible support to 4.0.0

## 20210413.1.0 - 2021-04-13

  - Packaging by Packer Docker builder and Ansible provisioner in single
    layer
  - Handle `ENTRYPOINT` with
    [catatonit](https://github.com/openSUSE/catatonit)
  - Handle `CMD` with SSHD
