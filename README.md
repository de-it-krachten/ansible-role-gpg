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

# Steps/phases to execute
gpg_install: true
gpg_generate_key: false
gpg_import_seckey: false
gpg_import_pubkey: false

# Default GNUPG home
gpg_home_default: "{{ ansible_local['users_ext'][gpg_user_name]['home'] }}/.gnupg"

# List of packages
gpg_packages:
  - gpg
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
- name: sample playbook for role 'gpg' pre playbook
  ansible.builtin.import_playbook: converge-pre.yml
  when: molecule_converge_pre is undefined or molecule_converge_pre | bool

- name: sample playbook for role 'gpg'
  hosts: all
  become: "yes"
  roles:
    - deitkrachten.facts
  tasks:

#    - name: Include role 'gpg'
#      ansible.builtin.include_role:
#        name: gpg
#      vars:
#        gpg_install: true
#        gpg_generate_key: true
#        gpg_import_seckey: false
#        gpg_import_pubkey: false
#        gpg_user_name: gpguser1
#        gpg_user_realname: gpguser1
#        gpg_user_comment: gpguser1
#        gpg_user_email: gpguser1@localhost
#        gpg_user_passphrase: Abcd1234

    - name: Include role 'gpg'
      ansible.builtin.include_role:
        name: gpg
      vars:
        gpp_install: false
        gpg_generate_key: false
        gpg_import_seckey: true
        gpg_import_pubkey: false
        # private key import
        gpg_user_name: gpguser2
        gpg_user_email: gpguser3@localhost
        gpg_seckey: gpguser3.sec

    - name: Include role 'gpg'
      ansible.builtin.include_role:
        name: gpg
      vars:
        gpp_install: false
        gpg_generate_key: false
        gpg_import_seckey: false
        gpg_import_pubkey: true
        # private key import
        gpg_user_name: gpguser2
        gpg_user_email: gpguser4@localhost
        # public key import
        gpg_recipient: gpguser4@localhost
        gpg_pubkey: gpguser4.pub
</pre></code>
