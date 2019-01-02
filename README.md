# Ansible
Ansible Playbooks

MAAS Deployments
Deployment with ansible
1. Edit the hosts file: /etc/ansible/hosts
2. Add new servers under the agents list [agents] and pound(comment) out prior deployments.
2a. You could add a section called [newservers] then drop all new servers there and edit the playbooks to target the newservers group instead, then move all servers to the [agents] section when done.  If doing that, i would probably add [masters] and [lbagents] as well to ensure all are added to properly named sections based on what the servers do.
3. Check MAAS interface for the NIC interface types ( eno / enp / ens / eth / etc.. ) and note it.
NOTE: if you have different types of NICs, then you will have to divide up the deployment based on the NIC type as the playbooks are specific to NIC type.
4. Run ansible-playbook newserver-<NICTYPEHERE>.yml
5. When it finishes, the server is ready for mesosphere ( or other things )



Ceph Deployments ( files start with Ceph in the name )
1. Edit the hosts file: /etc/ansible/hosts
2. Add five sections
[newservers]
[monprimary]
[mons]
[osds]
[rgws]
3. Place all new servers except the primary admin node under [newservers] with this format 'servername ansible_host=x.x.x.x' ( replace x's with server ip ).  Add the primary admin node under [monprimary] section with the same format.
4. Run ansible-playbook ceph_mon_primary.yml first and ONLY once.
5. Run ansible-playbook ceph_new_server.yml then after completion, move all the servers to their appropriate section in the ansible hosts file.
6. Run ansible-playbook ceph_hostsfile.yml
7. When it finishes, the servers are ready for ceph deployment using ceph deploy ( or manual deployment )
8. if you need to add more servers later, just run step 5 & 6 again ( step 6 can be run when you are ready )
