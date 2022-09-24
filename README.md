# OpenVPN Ansible playbook

A playbook to manage a PKI for OpenVPN

```sh
sh run.sh
```
## What does this playbook do?

NOTE: for commodity, we create the whole PKI on the same server. You should rather have dedicated CA (validating and signing certs) and the vpn (run openvpn) servers

* install easyrsa `3.0.8` in a dedicated `easyrsa_home`dir
* init the PKI
* generate `ca.crt` and `ca.key`
* generate `server.key` and `server.req`
* sign `server.req` and create `server.crt`
* generated pre-shared `ta.key`
* template `server.conf` and `client.base.conf`
* generate `<client>.req` and `<client>.key` for non already existing clients
* sign `<client>.req`  create `<client.cert>` for non already existing clients
* generate client config files
* copy client config files to localhost's `openvpn_client_configs_dest`
