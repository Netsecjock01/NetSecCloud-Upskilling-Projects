# Homelab Projects - Linux System Administration

*(This is a work in progress subject to updates,changes,revisions, etc...)

Below are hands-on task exercises I researched/complied, among pthers, and my part of my self-directed, personal and experimental IT homelab projects to help build/develop practical skillsets thru "tinkering" particularly in features, funtionalities or use cases in the area of comptuer system administration as well as topics on computer networking, cybersecurity, virtualization, cloud computing/devops, among others, as well as to help supplement/reinforce theoritical concepts, technical courses and related training I have undertaken or am currently taking in line with a favorite mantra, "Familiarity breeds mastery". It will be subject to modifications/updates periodically as my schedule or time permits:

**Linux SysAdmin**
*(#CTTO source: https://www.reddit.com/r/linuxadmin/comments/2s924h/comment/cnnw1ma/)* 

Do all tasks below and you will be fully exposed to every aspect of Linux Enterprise systems administration:
1. Set up a KVM hypervisor (Status: Pending). KVM hypervisor: a beginners’ guide & installing KVM on Ubuntu Linux: https://ubuntu.com/blog/kvm-hyphervisor

2. Inside of that KVM hypervisor, install a Spacewalk server. Use CentOS 6 (note: Try also CentOS Stream 9 or newer Rocky Linux) as the distro for all work below. (For bonus points, set up errata importation on the CentOS channels, so you can properly see security update advisory information.) (Status: Pending)

3. Create a VM to provide named and dhcpd service to your entire environment. Set up the dhcp daemon to use the Spacewalk server as the pxeboot machine (thus allowing you to use Cobbler to do unattended OS installs). Make sure that every forward zone you create has a reverse zone associated with it. Use something like "internal.virtnet" (but not ".local") as your internal DNS zone. (Status: Pending)

4. Use that Spacewalk server to automatically (without touching it) install a new pair of OS instances, with which you will then create a Master/Master pair of LDAP servers. Make sure they register with the Spacewalk server. Do not allow anonymous bind, do not use unencrypted LDAP. (Status: Pending)

5. Reconfigure all 3 servers to use LDAP authentication. (Status: Pending)

6. Create two new VMs, again unattendedly, which will then be Postgresql VMs. Use pgpool-II to set up master/master replication between them. Export the database from your Spacewalk server and import it into the new pgsql cluster. Reconfigure your Spacewalk instance to run off of that server. (Status: Pending)

7. Set up a Puppet Master. Plug it into the Spacewalk server for identifying the inventory it will need to work with. (Cheat and use ansible for deployment purposes, again plugging into the Spacewalk server.) (Status: Pending)

8. Deploy another VM. Install iscsitgt and nfs-kernel-server on it. Export a LUN and an NFS share. (Status: Pending)

9. Deploy another VM. Install bakula on it, using the postgresql cluster to store its database. Register each machine on it, storing to flatfile. Store the bakula VM's image on the iscsi LUN, and every other machine on the NFS share. (Status: Pending)

10. Deploy two more VMs. These will have httpd (Apache2) on them. Leave essentially default for now. (Status: Pending)

11. Deploy two more VMs. These will have tomcat on them. Use JBoss Cache to replicate the session caches between them. Use the httpd servers as the frontends for this. The application you will run is JBoss Wiki. (Status: Pending)

12. You guessed right, deploy another VM. This will do iptables-based NAT/round-robin loadbalancing between the two httpd servers. (Status: Pending)

13. Deploy another VM. On this VM, install postfix. Set it up to use a gmail account to allow you to have it send emails, and receive messages only from your internal network. (Status: Pending)

14. Deploy another VM. On this VM, set up a Nagios server. Have it use snmp to monitor the communication state of every relevant service involved above. This means doing a "is the right port open" check, and a "I got the right kind of response" check and "We still have filesystem space free" check. (Status: Pending)

15. Deploy another VM. On this VM, set up a syslog daemon to listen to every other server's input. Reconfigure each other server to send their logging output to various files on the syslog server. (For extra credit, set up logstash or kibana or greylog to parse those logs.) (Status: Pending)

16. Document every last step you did in getting to this point in your brand new Wiki. (Status: Pending)

17. Now go back and create Puppet Manifests to ensure that every last one of these machines is authenticating to the LDAP servers, registered to the Spacewalk server, and backed up by the bakula server. (Status: Pending)

18. Now go back, reference your documents, and set up a Puppet Razor profile that hooks into each of these things to allow you to recreate, from scratch, each individual server. (Status: Pending)

19. Destroy every secondary machine you've created and use the above profile to recreate them, joining them to the clusters as needed. (Status: Pending)

20. Bonus exercise: Create three more VMs. A CentOS 5, 6, and 7 machine. On each of these machines, set them up to allow you to create custom RPMs and import them into the Spacewalk server instance. Ensure your Puppet configurations work for all three and produce like-for-like behaviors. (Status: Pending)

--------------------------------------------------< TO BE CONTINUED... MORE TO COME >.....................................................................
