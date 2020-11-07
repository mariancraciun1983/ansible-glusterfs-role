<h1 align="center">GlusterFS cluster ansible role</h1>
<br />

<div align="center">
  <a href="https://travis-ci.com/mariancraciun1983/ansible-glusterfs-cluster">
    <img src="https://travis-ci.com/mariancraciun1983/ansible-glusterfs-cluster.svg?branch=master" alt="Build Status" />
  </a>
  <a href="https://galaxy.ansible.com/mariancraciun1983/glusterfs_cluster">
    <img src="https://img.shields.io/ansible/role/51683" alt="Ansible Galaxy" />
  </a>
  <a href="https://galaxy.ansible.com/mariancraciun1983/glusterfs_cluster">
    <img src="https://img.shields.io/ansible/quality/51683" alt="Ansible Quality Score" />
  </a>
  <a href="https://opensource.org/licenses/MIT">
    <img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="MIT License" />
  </a>
</div>
<br />

Ansible role to configure a GlusterFS cluster.


## Introduction

GlusterFS is a network filesystem which can use multiple storage mediums and combine them into a replicated and scalable filesystem.

This role will require at least 3 servers in order to satisfy the replication quorum.


### Ansible
This role was tested against Ansible version 2.8 2.9 2.10 .
The supported platforms are
  - Ubuntu
    - focal
    - bionic
    - xenial

## Variables
Configuration example
```yaml
group_vars:
  all:
    gluster_bricks:
      - brick_dir: /gluster/brick1 # location where to store the brick on each server
        mount_dir: /mnt/brick1 # leave this empty if you don't want to mount it too
        brick_name: brick1
        # number of bricks must be a multiple of replica count, but a min of 2
        # 2 for 2 or 4 or 6 bricks, 3 for 3 or 6 bricks..etc
        brick_replicas: 2
```

If you want to use an internal network
```yaml
group_vars:
  all:
    gluster_use_internal_ip: true
host_vars:
  node1:
    internal_ip: 10.0.0.1
  node2:
    internal_ip: 10.0.0.2

```

## Testing

Molecule with docker is being used.

Running the tests:
```bash
pipenv run molecule test
```