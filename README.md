In this mini project, I created a basic domain network using two virtual machines inside Oracle VirtualBox, a tool that allows us to run multiple operating systems on
the same physical machine. One virtual machine was configured as a Domain Controller running Windows Server 2019, and the other as a client computer running
Windows 10 Professional.

Network Configuration
Both virtual machines were set to use the Bridged Adapter networking mode. This mode allows each VM to act as if it were a separate physical device on the same
local network as the host PC. As a result, both machines received their own IP addresses automatically from the router via DHCP (Dynamic Host Configuration
Protocol), so there was no need to assign static IPs manually.

Installing and Promoting the Domain Controller
After installing Windows Server 2019, I used the built-in tool called Server Manager to add the role called Active Directory Domain Services (AD DS). This role
enables the server to handle authentication, user and group management, and control over devices on the network using Active Directory (AD) — a directory service
developed by Microsoft.

Once the role was installed, I followed the wizard to promote the server to a Domain Controller. This means that the server became the central authority for a new
network domain.

During this process:

I selected the option to create a new forest (a forest is the top-level container in Active Directory).

I named the domain gk.local, which is a private domain name used only within the local network.

I also set a Directory Services Restore Mode (DSRM) password, which is used to recover Active Directory in case of system failure.

I kept the default NetBIOS domain name (GK), which is a simplified name used for legacy systems that don't support full domain names.

The system then restarted to apply the changes, and the Domain Controller was ready.

Windows 10 Client: Joining the Domain
On the Windows 10 Professional virtual machine, I made sure it was also set to Bridged Adapter mode so that it could communicate with the server. After confirming
that both machines could ping each other (i.e., send and receive network packets), I proceeded to join the Windows 10 machine to the domain.

This was done by:

Going to System Properties → Change Settings under Computer Name

Choosing to join a domain instead of a workgroup

Entering gk.local as the domain name

After entering the domain administrator credentials (set earlier during the domain setup), the Windows 10 machine successfully joined the domain. Upon restart, it
could now log in using domain credentials managed by the server.

The client machine appeared on the domain as WINDOWS10KANAKISG, and from the server's Active Directory interface (Active Directory Users and Computers), I could
see and manage it as part of the domain network.

If anyone wants to review this setup or replicate it, I can share the VM files or document everything step-by-step. For any questions (e.g. admin passwords or
configuration details), feel free to contact me via email. 

Note:
During the setup, the Windows Defender Firewall was temporarily disabled on both the server and client machines to ensure that network communication (such as ping
and domain joining) would not be blocked. This step was taken for testing purposes within a controlled virtual lab environment. In a real-world deployment, proper
firewall rules should be configured instead of disabling it entirely.
