# terraform-libvirt

Terraform template to automatically deploy an ubuntu system with some initial configuration topics

## Configuration Cloud Init file

It is needed the configuration of the `cloud_init.cfg` file, specially related to passwords and access key.
See the content below: 

```
chpasswd:
  list: |
     root: <root>
  expire: False

users:
  - name: fla
    ssh_authorized_keys:
      - ssh-rsa AAAA...
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    passwd: <pass> 
    shell: /bin/bash
    groups: wheel
```

In case of _root_ and _passwd_, it is needed the configuration of the proper password. It can be generated through
the execution of the following command:

```
$ mkpasswd --method=SHA-512
```

In case of _ssh_authorized_keys_, in order to generate a new ssh key, using your email address, execute the following
command:

```
$ ssh-keygen -t ed25519 -C "nedmoh.cloud"
```

If you are using a legacy system that doesn't support the Ed25519 algorithm, use:

```
$ ssh-keygen -t rsa -b 4096 -C "nedmoh.cloud"
```

Copy the content of the id_rsa.pub file starting with "ssh-rsa AAAA..." and finishing with the email addrress
"nedmoh.cloud".
