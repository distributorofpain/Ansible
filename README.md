# Ansible
Ansible Playbooks

Deployment with ansible
1. edit the hosts file: /etc/ansible/hosts
2. add new servers under the agents list and pound(comment) out prior deployments.
3. Check MAAS interface for the NIC interface types ( eno / enp / ens / eth / etc.. ) and note it.
  a. if you have different types of NICs, then you will have to divide up the deployment based on the NIC type as the playbooks are specific to NIC type.
    i. just pound/comment out the entries for servers with different types
4. run ansible-playbook newserver-<NICTYPEHERE>.yml
5. when it finishes, the server is ready for mesosphere ( or other things )
