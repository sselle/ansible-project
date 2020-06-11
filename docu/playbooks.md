### limt playbook to defined group or host
    ansible-playbook playbook.yml --limit webservers
    ansible-playbook playbook.yml --limit xyz.example.com

### get all hosts affected by playbook
    ansible-playbook playbook.yml --list-hosts

### execute playbook as user
    ansible-playbook playbook.yml --user=johndoe

### store command output in variable
    - name: Get UUID
      shell: >
          blkid | grep xvdb |
          sed -n 's/.*UUID=\"\([^\"]*\)\".*/\1/p'
      register: uuid

### print debug messages
  - name: print debug message
    debug:
      msg: "{{uuid.stdout}}"