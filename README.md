Ansible activate
```
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Keygen
```
ssh-keygen -q -t rsa -f ./keys/id_rsa -b 4096 -C "" -N ""
```

Init
```
ansible-playbook create-user.yaml -e "ansible_user=root" --ask-pass
ansible-playbook lock-root.yaml
```
