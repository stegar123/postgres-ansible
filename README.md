Steps:

1. install ansible on management host(make sure to use latest version)
  https://www.cyberciti.biz/faq/how-to-install-and-configure-latest-version-of-ansible-on-ubuntu-linux/    

2. Clone the repository:
```console
  git clone https://github.com/stegar123/postgres-ansible.git && cd postgres-ansible
```

3. Change the ip address and credentials of remote hosts where postrgress will be installed (now is random: 5.5.5.5)<br />
   file: hosts/inventory

4. Execute playbook
 ```console
   ansible-playbook postgres-ansible.yml 
```

5. Install psql on your management host <br />
   Ubuntu package: postgresql-client
   
7. Connect to database ans check data in testtable table <br />
   The password you will find in group_vars/postgres
  
```console
#psql -h 5.5.5.5  -U testdbuser testwindsor 
Password for user testdbuser: 
psql (12.19 (Ubuntu 12.19-0ubuntu0.20.04.1), server 16.3 (Ubuntu 16.3-1.pgdg24.04+1))
WARNING: psql major version 12, server major version 16.
         Some psql features might not work.
SSL connection (protocol: TLSv1.3, cipher: TLS_AES_256_GCM_SHA384, bits: 256, compression: off)
Type "help" for help.

testwindsor=> select * from testtable;
 id | num |     stories     
----+-----+-----------------
  1 |   0 | 20240716212614Z
  2 |   1 | 20240716212614Z
  3 |   2 | 20240716212614Z
  4 |   3 | 20240716212614Z
  5 |   4 | 20240716212614Z
(5 rows)

testwindsor=> 
```

   
Keep in mind:

 1. It supported just Ubuntu 22.04
 2. Passwords are not secured - usually they are pushed into a vault or at least they must be used with Ansible Vault.
 3. All tests were performed using a remote host that is accessible via the internet. Your external IP address will be used to configure the firewall and PostgreSQL.
