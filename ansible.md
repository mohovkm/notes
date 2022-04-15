### run playbook with env vars and asking sudo pass
```bash
ansible-playbook \
--inventory=hosts \
postgres.yml \
-e postgres_owner_username=POSTGRES \
-e postgres_owner_password=PASSWORD \
--ask-become-pass
```

### send file via ansible job:
```yml
- name: Get file from server
  uri:
    url: "{{ url }}:{{ port }}/application/{{ item | basename }}"
    method: GET
    body: "{{ lookup('file','{{ item }}') }}"
    force_basic_auth: yes
    status_code: 404
    body_format: json
  with_fileglob: "{{ tmp_dir }}/configs/*"
  register: get_code_result
  ignore_errors: true

- name: Send file to server
  uri:
    url: "{{ url }}:{{ port }}/application/{{ item.item | basename }}"
    method: POST
    body: "{{ lookup('file','{{ item.item }}') }}"
    force_basic_auth: yes
    status_code: 201
    body_format: json
  with_items:
      - "{{  get_code_result.results }}"
  when: item.status == 404
  register: code_result
  until: code_result.status == 201
  retries: "{{ uri_retries }}"
  delay: "{{ uri_delays }}"
```

