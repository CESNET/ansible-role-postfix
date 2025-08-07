postfix
==========

Installs

Role
-------------

 - **postfix_myhostname:** -
 - **postfix_mydomain:** - "{{ postfix_myhostname }} "
 - **psotfix_myorigin:** - "{{ postfix_mydomain }} "
 - **postfix_relayhost:** - ""
    
 - **use_certs:** - false
 - **use_login:** - false    
 - **postfix_smtp_tls_cert_file:** - ""
 - **postfix_smtp_tls_key_file:** - ""
 - **postfix_smtp_tls_security_level:** - "encrypt"

 - **postfix_smtp_password:** - ""
 - **postfix_smtp_username:** - ""

 - **postfix_canonical_name:** - 
 - **postfix_canonical_email:** - 

 - **postfix_generic_name:** - 
 - **postfix_generic_email:** - 

 - **postfix_for_docker_bridge_network_name:** - ""

 - **postfix_sasl_passwd:** - "{{ postfix_relayhost_cesnet }} {{ postfix_smtp_username }}:{{ postfix_smtp_password }}" 