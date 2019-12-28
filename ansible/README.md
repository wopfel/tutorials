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

Running more tasks depending on a condition: block

```
- name: Block section
  block:
    - name: First task
      ansible_task_or_someting: ...
    - name: Second task
      ansible_task_or_someting: ...
  when: ... condition ...
```

Delete multiple files, specified by a file glob pattern

```
- name: Find all files by glob pattern
  find:
    paths: /path/to/files
    patterns: "*.bkp"
  register: file_list
- name: Remove matched files
  file:
    path: "{{ item['path'] }}"
    state: absent
  with_items: "{{ file_list['files'] }}"
```

