[![CI](https://github.com/de-it-krachten/ansible-role-wordpress_docker/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-wordpress_docker/actions?query=workflow%3ACI)


# ansible-role-wordpress_docker

Sets up a Wordpress instance using Docker.<br>
This consists of Wordpress/PHP/MySQL/nginx<br>



## Dependencies

#### Roles
None

#### Collections
- community.general

## Platforms

Supported platforms

- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- RockyLinux 8<sup>1</sup>
- RockyLinux 9<sup>1</sup>
- OracleLinux 8<sup>1</sup>
- OracleLinux 9<sup>1</sup>
- AlmaLinux 8<sup>1</sup>
- AlmaLinux 9<sup>1</sup>
- Debian 10 (Buster)<sup>1</sup>
- Debian 11 (Bullseye)<sup>1</sup>
- Ubuntu 18.04 LTS<sup>1</sup>
- Ubuntu 20.04 LTS<sup>1</sup>
- Ubuntu 22.04 LTS<sup>1</sup>
- Fedora 36<sup>1</sup>
- Fedora 37<sup>1</sup>
- Alpine 3<sup>1</sup>
- Docker dind (CI only)

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# Retrieve SSL certificate from let's encrypt
wordpress_certbot: true

# Custom SSL certificate
# wordpress_ssl_key: /path/to/key
# wordpress_ssl_certificate_chain: /path/to/certificate/chain

# Max upload size
wordpress_max_upload_size: 100M
</pre></code>




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'wordpress_docker'
  hosts: all
  become: "yes"
  vars:
    mysql_root_password: wordpress
    mysql_user: wordpress
    mysql_password: wordpress
    mysql_database: wordpress
    wordpress_certbot: False
    wordpress_domain: example.com
    wordpress_docker_data: /export/docker/wordpress
    wordpress_db_name: wordpress
    wordpress_db_user: wordpress
    wordpress_db_pwd: wordpress
    letsencrypt_email: "info@{{ wordpress_domain }}"
    letsencrypt_domain: "{{ wordpress_domain }}"
    letsencrypt_domains: "{{ [ wordpress_domain ] }}"
  roles:
    - deitkrachten.showinfo
    - deitkrachten.openssl
  tasks:
    - name: Include role 'wordpress_docker'
      ansible.builtin.include_role:
        name: wordpress_docker
</pre></code>
