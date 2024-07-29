win_users
=========

Create local users and ensure that they are active.
I use it to ensure that a local administrator user exists with a complex, random password.

Requirements
------------

This role is built to be used with Ansible oder SSH on Windows.

Notes
-----

Please be aware that this role is not very security oriented! The password should come from some secure location since the module is using it in plaintext. Also the account will not have to change the password, is unlocked and enabled. And the password will be reset to the one in this list.
The Ansible module uses the following settings to configure the user:
```yaml
state: present
account_expires: never
account_locked: false
account_disabled: false
password_expired: false
update_password: always
user_cannot_change_password: true
```

Role Variables
--------------

| Name                   | Comment                   | Default value |
|------------------------|---------------------------|---------------|
| win_users_users        | List of users to be added | `[]`          |

The `win_users_users` variable has a list of the following keys:

| Name        | Comment                                |
|-------------|----------------------------------------|
| name        | The username                           |
| fullname    | The full name                          |
| password    | The password (yes, this is plaintext!) |
| description | The description of the user            |
| groups      | A list of groups the user should be in |

This is a example with two local users to be added.

```yaml
win_users_users:
  - name: john
    fullname: John Doe
    password: SuperSecretPassword123
    description: John the local admin
    groups:
      - Users
      - Administrators
  - name: hans
    fullname: Hans Muster
    password: SuperSecretPassword456
    description: hans the local user
    groups:
      - Users

```

Example Playbook
----------------
```yaml
- name: Add local users
  hosts: windows
  roles:
    - role: oxivanisher.windows_desktop.win_users
```

License
-------

BSD

Author Information
------------------

This role is part of the [oxivanisher.windows_desktop](https://galaxy.ansible.com/ui/repo/published/oxivanisher/windows_desktop/) collection, and the source for that is located on [github](https://github.com/oxivanisher/collection-windows_desktop).
