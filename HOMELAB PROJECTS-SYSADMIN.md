# Homelab Projects - System Administration
*(*This is a work in progress subject to updates,changes,revisions, etc...)*

Below are hands-on task exercises I researched/complied, among pthers, and my part of my self-directed, personal and experimental IT homelab projects to help build/develop practical skillsets thru "tinkering" particularly in features, funtionalities or use cases in the area of comptuer system administration as well as topics on computer networking, cybersecurity, virtualization, cloud computing/devops, among others, as well as to help supplement/reinforce theoritical concepts, technical courses and related training I have undertaken or am currently taking in line with a favorite mantra, "Familiarity breeds mastery". It will be subject to modifications/updates periodically as my schedule or time permits:

A. **Windows SysAdmin**
*(#CTTO source: https://www.reddit.com/r/sysadmin/comments/3z7qd9/practice_to_become_a_windows_sysadmin/)*

Do the exercises below. One skill builds on another skill. Start with the basics:
1. Construct a closed virtual network. I used VMware Workstation hypervisor to accomplish this and this assumes windows Server 2012R2 VM (Try the newer Windows Server 2019 VM). Also, for this purposes of this lab, turn off the Windows firewall. In real life, you'll need to open ports as you see fit. In some networks, it's standard that all servers have their firewalls turned off. It really depends on your environment and what rules they follow.

2. Create two networks/VLANs (desktops and servers)

3. Install Windows Server (VM or standard hardware dealer's choice) GUI Mode.

4. Set up the server as a basic router between the two networks. You'll need 2 NICs to accomplish this (NOTE: unless you have a really good reason for this, you will never do this in a production environment. But because this is a lab situation in VMware Workstation and because the product does not support routing between networks, you'll need to put something in place very basic. Windows routing will get the job done and will be on an MCP exam)

5. Install another server, single NIC on the server VLAN

6. Create your first AD domain controller. Install this in GUI mode

7. Create another server but this time make it a core server. Make it a domain controller

8. Test AD replication via the gui and cmd.

9. Create an organizationla unit (OU) for your workstations, create an OU for your users, and an OU for groups. From now on, any new computer or new user account must go into their respective OU. DO NOT MOVE THE DOMAIN CONTROLLERS FROM THE DOMAIN CONTROLLER OU.

10. Check out DNS. Do you have a Reverse Lookup zone? No? Then set it up.

11. Check out DNS. Records can get old and out of date and will screw up name to IP resolution. Make it so that scavenging happens automatically.

12. You need to block Facebook.com via windows DNS. Make it so that when a DNS look up is performed, computers use a loop back address. Test this via cmd to make sure it resolves as expected.

13. Setup DHCP on the first domain controller.

14. Setup a scope to hand out IPs for the Desktop VLAN. Make it so that this DHCP scope will be able to give endpoints the information they need networking wise to join a domain

15. Install a Windows 7 or newer PC on the desktop VLAN

16. Your desktop's aren't getting IPs. Why? (hint: it's a routing/broadcast/relay issue)

17. Join that desktop to the domain

18. Now that you're getting IPs from your DHCP server, configure DHCP clustering. Loadbalancing or failover is your choice. Now test it.

19. Create a non-domain admin account in AD. Fill out the whole profile once the account is created.

20. Login to that desktop as a regular AD user and an Admin user. Try to install software under the non-admin account first and then the admin account. What's the difference?

21. Create another non-admin account. Make this non-admin user a local admin on that computer. Who else is also a local admin before you make any changes,

22. Review the attributes of that account in AD. You'll need advanced features for this.

23. Create an AD group. Add the first non-admin account to this group.

24. On that desktop, install the RSAT tools so you can remotely manage another computer

25. Setup remote management on the core server so that it can be managed from the MMC of another computer (there are a number of ways to do this)

26. Find out what server is holding the Flexible Single Master Operation (FSMO) roles via the gui and the command prompt.

27. Split the FSMO roles between the servers. Try to keep forest level and domain level roles together.

28. On one of the domain controllers, create a file share set it so that only administrators and the second non admin account have access to it. Create another folder and give only the AD group you created permissions.

29. Use group policy to map both shares as network drives as a computer policy to the desktops.

30. Login to the desktop as the first domain user. Do you see the network drive mapped in windows explorer? No? Use gpresult to find out why. If you do see it, try to access the drive. You should be denied if you set permissions correctly. Login as the second domain user, they should be able to open the mapped drive.

31. What if the account in the group tries to access the second drive? You should be able to get in.

32. Login to the workstation as the second non-admin account. You should not have access to this drive because you are not in the group. Do not log off. Add this account to the group. Can you access the drive now? No? Logoff and login back in. Can you access the drive now?

33. Remove the share from the domain controller. We don't like putting shares on domain controllers if we don't have to.

34. Build out another two servers and join it to the domain as member servers.

35. Install DFS and File server roles/features on both servers.

36. Create a file share on bother servers with the same folder name. Create files on both servers. Make sure they are different. (i.e server1 will have "TextDoc01", server 2 will have "TextDoc02" in their shares).

37. Create a DFS name space. Add those shares to the name space.

38. On a domain joined work station, navigate to the DFS namespace you created. You should be able to see both files.

39. Create a DFS Replication group. Make it so that you have two way replication. You should now see both files on both servers. Make a change on one server and see if it replicates to another server. Does it work? Great. (you can shut down the file servers for now if you want or use them for the next step)

40. Create another server, join it to the domain, install Windows Deployment Service (WDS) and Windows Server Update Service (WSUS). You can choose to use the file servers you've already created instead of building out another VM. You only need one file server.

41. Configure WDS so that you can PXE boot to it on the network. Make any required changes to routing and DHCP if need be.

42. Upload an image to WDS for PXE deployment. Use WAIK and sysprep if you need to. (I haven't done this in the long time so you might not need sysprep anymore with WAIK, look it up)

43. Create a new desktop VM but do not install an OS on it. Instead tell it to perform a PXE boot when you turn it on, have it install the OS from here.

44. Configure WSUS so that you will only download Security updates for the desktop and server OS's ( highly recommend that you do not download any updates if you have access to the internet from this server)

45. Bonus points, install WSUS on another server and create a downstream server)

46. Create some groups in WSUS. Servers and workstations will do nicely.

47. Create a new group policy that points workstations into the WSUS workstation group, points to WSUS for updates, and stop workstations from automatically downloading updates.

48. Read up on approving and pushing updates since the current assumption is that there are no updates to be pushed in this enclosed test network since there is no internet access to down load them. I believe there is a way to manually add updates to WSUS but I'm a bit foggy on that. Research it.

49. Do the same for servers.

50. create a new AD user via powershell.

51. Create a new AD group via powershell.

52. Print a list of all domain users and computers in powershell, names only

53. Use powershell to pull a list of users who have new york as their office. If no users have new york listed as their office, use powershell to set that attribute and then pull users who have new york as their office.

54. Remove a user account from AD using powershell

55. Add a user to a group using powershell

56. Provision new AD users via a CSV in powershell

***This is really only scratching the surface of a typical medium-large to enterprise level network. But this should be enough to get you started.

B. **Linux SysAdmin**
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

14.Deploy another VM. On this VM, set up a Nagios server. Have it use snmp to monitor the communication state of every relevant service involved above. This means doing a "is the right port open" check, and a "I got the right kind of response" check and "We still have filesystem space free" check. (Status: Pending)

15. Deploy another VM. On this VM, set up a syslog daemon to listen to every other server's input. Reconfigure each other server to send their logging output to various files on the syslog server. (For extra credit, set up logstash or kibana or greylog to parse those logs.) (Status: Pending)

16. Document every last step you did in getting to this point in your brand new Wiki. (Status: Pending)

17. Now go back and create Puppet Manifests to ensure that every last one of these machines is authenticating to the LDAP servers, registered to the Spacewalk server, and backed up by the bakula server. (Status: Pending)

18. Now go back, reference your documents, and set up a Puppet Razor profile that hooks into each of these things to allow you to recreate, from scratch, each individual server. (Status: Pending)

19. Destroy every secondary machine you've created and use the above profile to recreate them, joining them to the clusters as needed. (Status: Pending)

20. Bonus exercise: create three more VMs. A CentOS 5, 6, and 7 machine. On each of these machines, set them up to allow you to create custom RPMs and import them into the Spacewalk server instance. Ensure your Puppet configurations work for all three and produce like-for-like behaviors. (Status: Pending)

--------------------------------------------------< TO BE CONTINUED... MORE TO COME >.....................................................................
