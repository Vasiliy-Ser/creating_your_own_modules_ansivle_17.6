My module
=========

Create file



Role Variables
--------------

| Parameter       |  Default              | Description                     |
|-----------------|-----------------------|---------------------------------|
| file_path       |  /tmp/test_file.json  | File path                       |
| file_content    | "Test content"        | File content                    |
| file_mode:      |  "0644"               | Octal permissions (e.g. "0644") |



Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: my_module }

License
-------

MIT

Author Information
------------------

Padeev Vasiliy
