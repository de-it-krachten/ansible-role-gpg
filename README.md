[![CI](https://github.com/de-it-krachten/ansible-role-gpg/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-gpg/actions?query=workflow%3ACI)


# ansible-role-gpg

Installs gpg and manage keys



## Dependencies

#### Roles
- deitkrachten.facts

#### Collections
- community.general

## Platforms

Supported platforms

- Red Hat Enterprise Linux 7<sup>1</sup>
- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- CentOS 7
- RockyLinux 8
- RockyLinux 9
- OracleLinux 8
- OracleLinux 9
- AlmaLinux 8
- AlmaLinux 9
- Debian 10 (Buster)
- Debian 11 (Bullseye)
- Ubuntu 18.04 LTS
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- Fedora 36
- Fedora 37

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# GPG home directory
# gpg_home: $HOME/gnupg

# List of packages
gpg_packages:
  - gpg

# Key settings
gpg_userkey:
  key:
    type: "RSA"
    length: "4096"
  subkey:
    type: "RSA"
    length: "2048"
  name:
    real: "{{ gpg_user_realname }}"
    comment: "{{ gpg_user_comment }}"
    email: "{{ gpg_user_email }}"
</pre></code>

### defaults/family-Alpine.yml
<pre><code>
# List of packages
gpg_packages:
  - gpg
  - gpg-agent
</pre></code>




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'gpg'
  hosts: all
  become: "yes"
  vars:
    gpg_user_name: root
    gpg_user_realname: root
    gpg_user_comment: test key
    gpg_user_email: root@localhost
    gpg_user_passphrase: Abcd1234
  tasks:
    - name: Include role 'gpg'
      ansible.builtin.include_role:
        name: gpg
</pre></code>
