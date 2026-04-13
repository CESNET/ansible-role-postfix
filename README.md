postfix
==========

Ansible role for install MTA Postfix on Debian 11+. 

Role vars:
-------------

| Variable                                   | Description |
|--------------------------------------------|-------------|
| `postfix_myhostname`                       | Fully Qualified Domain Name (FQDN) used by Postfix to identify itself in SMTP communication. |
| `postfix_mydomain`                         | Domain name of the server; usually the part after the first dot in `myhostname`. |
| `postfix_myorigin`                         | Domain appended to outgoing mail without a domain; typically `{{ postfix_mydomain }}`. |
| `postfix_relayhost`                        | Optional SMTP relay through which all outgoing mail is sent (e.g., `[smtp.example.com]:587`). |
| `postfix_use_certs`                        | If `true`, enables TLS certificates for securing SMTP connections. |
| `postfix_use_login`                        | If `true`, enables SMTP authentication with username and password. |
| `postfix_smtp_tls_cert_file`               | Path to the TLS certificate file used by Postfix. |
| `postfix_smtp_tls_key_file`                | Path to the private key file used by Postfix. |
| `postfix_smtp_tls_security_level`          | TLS security mode for SMTP connections (e.g., `encrypt`, `may`). |
| `postfix_smtp_password`                    | Password for SMTP authentication. |
| `postfix_smtp_username`                    | Username for SMTP authentication. |
| `postfix_sasl_passwd`                      | SASL credentials for relay host in format: `relayhost username:password`. Built automatically as `{{ postfix_relayhost }} {{ postfix_smtp_username }}:{{ postfix_smtp_password }}`. |
| `postfix_canonical_email`                  | Email address used for canonical address mapping (rewriting sender email). |
| `postfix_generic_email`                    | Email address used for generic address mapping (rewriting recipient email). |
| `postfix_for_docker_bridge_network_name`   | Name of the Docker bridge network Postfix should bind to (if running inside Docker). |
| `postfix_testing_email`                    | Email for sending testing email. |



## Simple Example Playbook

```yaml
- hosts: all
  roles:
    - cesnet.postfix
```

## Example of More Complex Playbook

```yaml
- hosts:
    - "some-random-name.my-cloud.org"
  vars:
    postfix_myhostname: "mail.example.com"
    postfix_mydomain: "example.com"
    postfix_myorigin: "{{ postfix_mydomain }}"
    postfix_relayhost: "[smtp.relay.com]:587"
    use_certs: false
    use_login: true
    postfix_smtp_tls_cert_file: "/etc/ssl/certs/mail.crt"
    postfix_smtp_tls_key_file: "/etc/ssl/private/mail.key"
    postfix_smtp_tls_security_level: "encrypt"
    postfix_smtp_username: "relayuser_example"
    postfix_smtp_password: "supersecret"
    postfix_canonical_email: "noreply@example.com"
    postfix_generic_email: "test@example.com"
    postfix_for_docker_bridge_network_name: "postfix_network"
    postfix_sasl_passwd: "{{ postfix_relayhost }} {{ postfix_smtp_username }}:{{ postfix_smtp_password }}"   
    postfix_testing_email: testint@email.com
  roles:
    - cesnet.postfix
```
