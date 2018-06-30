Openwrt-openvpn
===============

This role makes a setup of openvpn on a openwrt router

Requirements
------------

It needs roles fabrizio2210/openwrt-uci, that contains the modules to perform uci settings and file operations, and role fabrizio2210/ansible-easy_rsa.

Role Variables
--------------

openwrt_openvpn_verb: verbosity log
openwrt_openvpn_comp_lzo: yes/no use compression
openwrt_openvpn_dev: tun or tap
openwrt_openvpn_proto: UDP or TCP
openwrt_openvpn_ping_restart: seconds after no ping it should restart
openwrt_openvpn_topology: type of topology (subnet...)
openwrt_openvpn_ping: seconds between ping

_Server_
openwrt_openvpn_server_name: little string to describe the server
openwrt_openvpn_server_port: UDP/TCP port to use for the server
openwrt_openvpn_server: (boolean) the target is a server? (you can run multiple times to setup once like a server and then like client)
openwrt_openvpn_server_host: the FQDN to contact the server 
openwrt_openvpn_push_routes: subnets to advise to the client
openwrt_openvpn_ping_timer_rem: use timer when a remote peer is connected

_Client_
openwrt_openvpn_client: (boolean) if client or not
openwrt_openvpn_client_name: little string to describe the client (useful if you have multiple clients and maybe one server on the target
openwrt_openvpn_remote_host: the FQDN of the server to contact when the target is client
openwrt_openvpn_remote_port: the UDP/TCP of the server to contact when target is client
openwrt_openvpn_persist_key: persist key over reload
openwrt_openvpn_persist_tun: persist interface over reload

Dependencies
------------

It depends on fabrizio2210/openwrt-uci and fabrizio2210/ansible-easy_rsa.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts:
      - openwrt-server
      gather_facts: no
      tasks:
      - name: Configure OpenVPN as a server on an openwrt router
        include_role:
          name: openwrt-openvpn
        vars:
          openwrt_openvpn_server: True
          openwrt_openvpn_server_name: 'TN'
          openwrt_openvpn_server_port: 1194
          openwrt_openvpn_server_host: myserver.no-ip.org
          openwrt_openvpn_static: false
          openwrt_openvpn_topology: 'subnet'
          openwrt_openvpn_server_subnet: "10.8.0.0"
          openwrt_openvpn_server_subnet_mask: "255.255.255.0"
          openwrt_openvpn_comp_lzo: 'no'
          openwrt_openvpn_push_routes:
            - "192.168.2.0 255.255.255.0"



License
-------

BSD

Author Information
------------------

I am Fabrizio W, a sys admin with a passion for comodity hardware.
