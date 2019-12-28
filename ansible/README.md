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

Run a task only if a file is present (or not present likewise)

`isreg`: regular file, `isdir`: directory

```
- name: Detect file stats
  stat:
    path: /path/to/file
  register: stat_result
- name: Do task if file exists
  ansible_task_or_something: ...
  when: stat_result.stat.isreg == True
```

