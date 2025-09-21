Install Rocky

```
sudo qemu-img convert -f qcow2 -O raw ./Rocky-10-GenericCloud-Base.latest.x86_64.qcow2 /dev/sdc
```
Reset password:
- Stop the countdown timer using up and down arrows
- Select the kernel to edit (usually the first one listed)
- Press e
- On the line that begins with linux, remove console and/or vconsole directives
- Add init=/bin/bash to the end of the line
- Press Ctrl-X
- mount -oremount,rw /
- passwd
- touch /.autorelabel
- /usr/sbin/reboot -f
- Log in with new password

Allow Root ssh
```
vi /etc/ssh/sshd_config
PermitRootLogin yes
```

Ansible activate
```
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
ansible-galaxy install -r ansible-requirements.yaml
```

Instalation
```
ansible-playbook 01-create-user.yaml -e "ansible_user=root" --ask-pass
ansible-playbook 02-host-init.yaml
ansible-playbook 03-rke2-install.yaml
```

Check
```
kubectl --kubeconfig keys/rke2.yaml get po -A
```

(Optional) Keygen
```
ssh-keygen -q -t rsa -f ./keys/id_rsa -b 4096 -C "" -N ""
```
