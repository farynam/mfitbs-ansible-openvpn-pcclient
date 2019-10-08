mfitbs-ansible-openvpn-pcclient
=========

Simple pc like client cert generator for OpenVpn. 

Requirements
------------

* Ansible 2.8.5
* Debian 10
* Debian 9

Role Variables
--------------

* server_port - ex. 1194
* proto: tcp
* cipher - ex. AES-256-CBC
* id_type - ex. IP or UDP
* easy_rsa_host - name of easyrsa host from inventory 
* clients - clients list

Dependencies
------------

* mfitbs-openvpn-easyrsa

Example Playbook
----------------

* Inventory


    [easyrsa]
    
    erh ansible_host=192.168.51.5 ansible_user=root ansible_password=qwerty ansible_ssh_common_args='-o StrictHostKeyChecking=no'
    
    [server]
    
    server ansible_host=192.168.51.4 ansible_user=root ansible_password=qwerty ansible_ssh_common_args='-o StrictHostKeyChecking=no'
    
    [client]
    
    client1 ansible_host=192.168.51.6 client_addr=10.8.0.2 client_mask=255.255.255.0 ansible_user=root ansible_password=qwerty ansible_ssh_common_args='-o StrictHostKeyChecking=no'
    


* Playbook:


    - name: Test Client
      hosts: erh
      roles:
      
        - role: farynam.mfitbs_openvpn_pcclient
        
          vars:
          
                server_port: 1194
            
                groups['server'][0]: 192.168.51.4
            
                proto: tcp
            
                cipher: AES-256-CBC
            
                id_type: IP
            
                easy_rsa_host: erh
            
                clients:
            
                - 1
                - 2
                - 3
                - 4
                - 5
              
      tasks:

License
-------

MIT

Author Information
------------------

Marcin Faryna
