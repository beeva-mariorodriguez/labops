# ansible

## directory layout

we will use a simple directory layout, just a playbook file under ansible/ and roles under ansible/roles
```
ansible/
        requirements.yml
        playbook.yml
        roles/
```     

## roles

leave small roles directly in the repo under roles/, for bigger roles we should have indepedent repositories

### requirements

describe needed roles in ansible/requirements.yml
```
- name: docker_ce
  src: https://github.com/beeva-mariorodriguez/ansible-docker_ce
```
and install with:
```sh
ansible-galaxy install -r ansible/requirements.yml -p ansible/roles/
```

