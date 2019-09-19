ansible-role-disk
=================

[![Build Status](https://travis-ci.org/kevincoakley/ansible-role-disk.svg?branch=master)](https://travis-ci.org/kevincoakley/ansible-role-disk)

Partition, Manage LVM, Format and Mount Disks for CentOS 7 and Ubuntu 18.04

Requirements
------------

None

Role Variables
--------------

See defaults/main.yml

Dependencies
------------

None

Example Playbook
----------------

    - name: Partition, Manage LVM, Format and Mount Disks on Linux
      hosts: disk
      become: yes
      become_method: sudo
    
      vars:
        parted:
          - device: /dev/vdc
            number: 1
            label: gpt
            state: present
        lvg:
          - vg: vg_test
            pvs: /dev/vdc1
        lvol:
          - vg: vg_test
            lv: lv_test
            shrink: no
            size: 100%FREE
        filesystem:
          - fstype: xfs
            dev: /dev/vg_test/lv_test
        mount:
          - path: /mnt/volume-test-1
            src: /dev/vg_test/lv_test
            fstype: xfs
            opts: defaults
        
      roles:
        - ansible-role-disk

License
-------

BSD

Author Information
------------------

Kevin Coakley (https://github.com/kevincoakley)