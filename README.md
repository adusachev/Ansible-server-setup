## Server configuration


### Create non-root user with sudo priveleges

```sh
ssh root@[SERVER_IP]
```

(on server) Create new user `www`:
```sh
adduser www
# create password for "www" user
```

(on server) Grant sudo priveleges to `www`:
```sh
adduser www sudo
```

(on host) Add ssh keys:
```sh
ssh-copy-id -i $HOME/.ssh/[SSH_KEY_NAME].pub www@[SERVER_IP]
```


---

### Configure Ansible

(on host)

```sh
vim hosts
# add your SERVER_IP and SSH_KEY_NAME
```

```sh
vim sudo_pass
# write sudo password for "www" user here
```
```sh
chmod go-rw sudo_pass
```

check that ansible is ready
```sh
ansible ubuntu -m ping
```

---

### Run playbooks

(on host)

Install packages:
```sh
ansible-playbook packages_playbook.yaml --become-password-file sudo_pass
```

Install docker:
```sh
ansible-playbook docker_playbook.yaml --become-password-file sudo_pass
```

Install zsh:
```sh
ansible-playbook zsh_playbook.yaml --become-password-file sudo_pass
```

---

to be continued..