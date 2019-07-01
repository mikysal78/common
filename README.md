<BS># Ansible role `common`

[![N|Solid](http://basilicata.ninux.org/images/Logo_Ninux_Basilicata_600-192.png)](http://basilicata.ninux.org)

Ruolo Common

## Installazione di Ansible su Debian
$ sudo apt-get install ansible
~~~

## host inventory
[common]
# Local
pdl ansible_connection=local ansible_user=root
# Remote
yourhost ansible_user=root ansible_port=22 ansible_host=youip

### Esempio definizione del playbook

```Yaml
- hosts: common
  become: "{{ sudo | default('yes') }}"
  roles:
    - common
  vars:
    # common
    common_ipv4_forward: 1
    common_ssh_port: 2400
    # variabili per ruolo common
    users:
      - name: michele
        authorized:
          - ./keys/michele.pub
      - name: nino
        authorized:
          - ./keys/nino.pub
      - name: marco
        authorized:
          - ./keys/hispanico.pub
      - name: federico
        authorized:
          - ./keys/federico-1.pub
          - ./keys/federico-2.pub
```

### Avvio del playbook

```
ansible-playbook -i hosts common.yml -l common

```

