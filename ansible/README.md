Ansible examples
================

Run a command only if a file (or glob pattern) doesn't exist

```
- name: Run a command only if a file doesn't exist
  command: cmd ...
  args:
    creates: /path/to/file
```

Run a command only if a file (or glob pattern) is present

```
- name: Run a command only if a file is present
  command: cmd ...
  args:
    removes: /path/to/file
```


