Domain Join
===========

An Ansible role for join hosts to Active Directory domain and local administrators management.

Requirements
------------

- Supported version of Ansible: 2.9 and highter.
- `pywinrm` is a python library for connection Ansible to Windows hosts via [WinRM](https://docs.ansible.com/ansible/latest/user_guide/windows_winrm.html).
- Supported platforms:
  - RHEL
    - 7
    - 8
  - Ubuntu
    - 18.04
    - 20.04
  - Debian
    - 10
    - 11
  - Windows
    - 2016
    - 2019

Role Variables
--------------

- `domain_join_dns_domain_name` DNS name of the domain to which the targeted host should be joined.
- `domain_join_domain_controllers` Domain controllers list.
- `domain_join_username` Username to use for enrollment.

  **Attention** If you use a non-administrator user, you'll need to delegate him rights to create and change `operating System` and `operatingSystemVersion` schema objects.

- `domain_join_password` Password for the specified `domain_join_username`.
- `domain_join_ou_path` Computer DN OU to join.
- `domain_join_admin_groups` A list of members present in the Administrators group.

Dependencies
------------

None.

Example Playbook
----------------

```yaml
---

- name: Join to Active Direcory domain
  hosts: all

  roles:
    - role: antmelekhin.domain_join
      domain_join_dns_domain_name: domain.local
      domain_join_domain_controllers:
        - dc-01.domain.local
        - dc-02.domain.local
      domain_join_username: Administrator
      domain_join_password: P@ssw0rd!
      domain_join_ou_path: OU=Servers,DC=domain,DC=local
      domain_join_admin_groups:
        - sysadmins
```

License
-------

MIT

Author Information
------------------

Melekhin Anton.
