**Project Overview**

This project entails simulating a corporate network using Oracle VirtualBox, featuring key steps such as establishing a Windows Server 2019 Domain Controller (DC), configuring networking, promoting the server to a domain controller, deploying Active Directory, installing a Remote Access Server (RAS/NAT) and DHCP server, and creating a Windows 10 client VM. These actions enable private network communication and internet access via the domain controller. The project showcases tasks like IP configuration, user account creation, and domain integration, serving as a comprehensive demonstration of a simulated corporate network environment for educational and testing objectives.

**Project Diagram**

![](https://lh3.googleusercontent.com/2SuLgIVwt8P-BxdAVPdpG3GVoyYeBWTL06fNavDuRMCl6t427EAg1jGhpDEuvlvFEzMrKlDaLmYDKCgJ51wKzR1QzxMStw3kdV2bZUuCrnElyi-vq0LbvuMwpd0RVKfogwjNWaB4VQQ7R5fX6CiC9Fw)

**Project Walkthrough**

1\. Initial Setup:

   - Begin by acquiring essential software components, including Oracle VirtualBox, Windows 10 ISO, and Windows Server 2019 ISO.

2\. Virtual Machine Provisioning:

   - Create the primary virtual machine in VirtualBox, designated as the Domain Controller (DC), which will serve as the foundation for the Active Directory infrastructure.![](https://lh5.googleusercontent.com/xGXVXzHkRYzEiabvg1-VIY06X5qbSQhC6ltCURbIvOYi_X_YgHdYYByAT2nC2qGrIvpTNRW755x46XYO2mjAq3Cx0Ca7J_JpALXQeJ0CNi76Czya_T98bS287Gd5DnfTJjwn2Q742DuZ_XV5vkYtcLo)

   - Configure the DC VM with dual network adapters, each assigned distinct roles: one facilitating external internet connectivity and the other establishing internal network communication.![](https://lh4.googleusercontent.com/fY5DiMc3dhOrnOHnz5BBrf93NjILFYyk2t87gIjhj4QmZc7yQ1PZ07UQyV-RpKY3OcFf5AGUtA24eycnsOkqroIp88w3KK1yuTBz0gagP87jha_4durIvphDA7wtajdZOAU-Dn-zHPVqALcE5uKL_0E)

This Network Adapter is attached to a NAT that will connect this virtual machine to the internet.

![](https://lh5.googleusercontent.com/NFfQq0oSb0BoboY_yT0WVacZCH9EXDJItGdkW1Go5FHc07TM1FGmsbeTC4NfcXY2RS4o_557_4oed0fNW0zPYPphFhn7Ph_mxmXqBci26vI7Ez8aCVqJe8y_DhB-Jq_3QVWzZiFSNEvShSrzzg5JyKw)

Another Network Adapter is added to the virtual machine to connect to the internal network.

3\. Operating System Deployment:

   - Deploy Windows Server 2019 onto the Domain Controller VM, ensuring a solid operating environment for subsequent configuration.

![](https://lh5.googleusercontent.com/fX_lyjh-2POun_Q6pfRX2tt_yiDzywr0i2-l7M3gruSeYWXOt-V-tJs0RPN_AAR4xiyyH_984yB59xwzTDQNUphevbziUpxiRgN0qBB1s2hIIC0OkCBaS4ROyzhKeiXg_1vSzZtpkPZxCc75gQw_Ees)

4\. Network Configuration:

   - Define precise IP addressing for the internal network segment, establishing seamless communication within the designated environment. Navigating to the Internal NIC IPv4 Properties, we assign the IP address and subnet mask for the NIC. No default gateway was specified because the Domain Controller itself will serve as the gateway, as it has two NICs- one for the internet and one for the internal network. For the DNS server, Active Directory will automatically install a DNS, so this server will use itself as the DNS server. For that reason, we use 127.0.0.1 for the DNS server, which is the self referencing address. 

![](https://lh5.googleusercontent.com/8fp6WZQy_DhmgEwUr4_rvDG2JPdpCqfFOBINCuExhrtm2qB2uNIkxS4i6V-8NKqRLmF6f1XsdWTC1tGjmjQwKnKU2sl7bsEoZJwkomAnjEu70iWwZaTGhN7ZOQ_oi0kD1B9MUbHJt0vIUzBTNY-B-kw)

   - Enable automatic IP assignment for the external network interface to seamlessly interface with the home network's IP allocation.

5\. Active Directory Implementation:

   - Execute the installation of Active Directory within the Domain Controller VM, establishing the foundational domain framework. Through the Server Manager interface, we can use the “Add roles and features” tab to download Active Directory onto the Domain Controller.![](https://lh6.googleusercontent.com/CSxhg0FlHNf8hsXsvZExK7w_suV7EyPcXb3J14fwX2vlmqb1BkWaO2LtJfyQQ8xfSZ_WQmi6GaFgAIYjgLipBGV8riPH4yyKwR6HgQsrdn4j3njeDX0tak5H4-pIM8lU-JCjo0XTgUnmfqsWu9JZTmc)

During deployment of Active Directory, we will create a specific domain name to finish establishing the domain. 

![](https://lh4.googleusercontent.com/951w-PnOUhuz1XHUZ6QwRCSfVZvHIdP6c5KOSExVrvYqxPCmXQS81eiUmHqc1qDzqHuXmBB0Z2ER0sPC-LRBjs--Bj8oX4b4JHS-WD17_VddrUMnxvnFpVYvhK6l9ODfP9KFHV64TUJnQslIRqKTxUk)

6\. RAS/NAT Integration:

   - Incorporate Remote Access Service (RAS) and Network Address Translation (NAT) functionalities to empower the private network with internet accessibility via the Domain Controller. This step is taken to enable secure and controlled internet connectivity for the private network by implementing Remote Access Service and Network Address Translation.

Through the “Add roles and features” tab on the Server Manager, Remote Access is installed on the Domain Controller.![](https://lh3.googleusercontent.com/HIfcAJyMVj7YToqe4xOrNXjy-JWzsGqelBCr_sgR_qMtltWj4AVoQMIgufKVVZOa1Pk6mWDVvSu38opzZtryjoTp5BDFuiQaEUqbxvPAYHhIsfvtmEfJI2IMgp3eSrLTzPtlKoWY1aO1hDENTOZAQ7Y)

Through the 'Tools' tab on the Server Manager, we can configure network address translation (NAT) on the domain controller, facilitating the translation of internal private IP addresses to a single public IP address when accessing the internet. This translation process adds an additional layer of security for devices within the private network

![](https://lh4.googleusercontent.com/YDMA9LuDxJu9jNn8ii40KyQKERpvqE4m-FzP86JuEjGQgyoCY_-nczVPC8FzBcuzsiiP3Xl7G_wHImOohdJo2FuL6JVj37Y_LAfkqwygbpciySRAfM7QytDkn_HxfipLoQgzfb3GWfigfP-wB79LwXE)

7\. DHCP Deployment:

   - Set up a Dynamic Host Configuration Protocol (DHCP) server within the Domain Controller, facilitating the automated provisioning of IP addresses to other Windows 10 VMs. Through the “Add roles and features” tab on the Server Manager, we can install a DHCP Server onto our Domain Controller. The DHCP server is responsible for automatically assigning IP addresses and other essential network configuration parameters (such as subnet masks, default gateways, and DNS server addresses) to devices within a private network.

![](https://lh5.googleusercontent.com/bQfhHI_87tlypWp51dyDEKKNl6BvB_LlPFd5zd-lZ7aum61fkDyh6DFNjUDtIMbI1RYsTRWmyAxIBR9zr808M4dJL5emUSxXatqdXHy_1bgr3E3qxfNrEsQsl35Pvgf3UP1SB8PfJUjGdf8qq7VnNmg)

Next, we will define the scope address range for the DHCP server, which is 172.16.0.100-200, and the subnet mask will be 255.255.255.0. 

![](https://lh6.googleusercontent.com/kxSK9eIijIlZcpkZmDizh62cR8zYNE-ibA7bfEqPPbbctYGmWueei9gPuqkIlHyU734H5IsRDe1J4DuD4XZm7TasjA10hPnzmmOLbD3QoKzWYEGUE7fRAvilFBAA8S3CvssFSjMcolw4F0mMQXyBhB8)

As for the default gateway of the DHCP server, we will use the IP address of the Domain Controller, as it has access to both the internal network and the internet. 

![](https://lh6.googleusercontent.com/sj4_XJBWwqeSzRpZou905R8p2ubeumJJNDlxk3dPRY5GlgZUApSh4u8rmrR2vkveC0pRsGVWZ8BgbTjwVwlBb_v7VYoFjGFbra1Q8-YF7QTCwMePSvPg8708pUWpd2Epi5vBnKGearl0EPRYKKyza5M)

Finally, we will use the Domain Controller’s IP address and domain name for the DHCP server. Using the DC's IP address as the DNS server for DHCP clients ensures reliable name resolution, seamless integration with Active Directory, efficient resource location, dynamic updates, centralized management, reduced network traffic, and improved network security for devices within the domain.

![](https://lh3.googleusercontent.com/Ak4gSIKhI05tTXidVrqx6qDUvU76kZSeCrKCqLuIIkiFUBp8LfrxEXHY6eNr3SEkSyN-hP6lelDpR5Pboxi2SBgaEbQMgnqqRgIyWqxdbGbdnHT8r1mMN77oXZhURMGXYAnKGkBYFCZZALWvWrb2Z2M)

8\. Automated User Population:

   - Employ a PowerShell script to streamline the process of generating a substantial user base, populating the Active Directory with a thousand user accounts. The script accesses names from a folder, names.txt, to create a username which consists of the first letter of an employee's first name and attaches it to their last name. 

![](https://lh6.googleusercontent.com/O3IfCTw15IEMNoPnSx4I7GSczdr6-TtMTicK-oq3aYClTvySMz8wToQqKyVke8p-6vWb-GnkLcCRLy4qYOBJPbD7iJeVyHsGW9BubGns5Ae9BCLsyho90bB5PZhhh_hKaTDslhNmIJDvSg2WcdupsAs)

Next, the script will fill out account details using previously defined variables. By doing this, the script is automating the creation of accounts. 

![](https://lh4.googleusercontent.com/nBkBkijsDkDH6Pc7CESqa_hDNCgx3rHYj7XhExbtMT9qKGnlrCogCVnjMxqYio-CleNvLJ0lZxFUjJo5W6uImef2BWHC33Oo-s9PxK-rjYIiUPSik3QK1yoNnMOXgDq-BC6VSMlBjnmLACL1FvzY7IA)

9\. Secondary Virtual Machine Configuration:

   - Create an additional virtual machine, installing Windows 10 to form a distinct endpoint within the domain. The second virtual machine is called ‘CLIENT1.’![](https://lh5.googleusercontent.com/JP6ArOZ4vcw4RLGI7gC7Rls45ZF4hmb2le5A8pRFl18EcaOwBSWI4Lh1wU7GAT4Hxu9D5JhFduvSMyn1dNj9TAyl_hR0rwedmTLyC2-f1VNADx2Np_NcbUhmAzzsmeU4_XaaXUepeVkRoXviNm30fsg)

On the second virtual machine, we will make sure the network adapter is attached to the internal network.  

![](https://lh3.googleusercontent.com/pnwiCYH86GlLqOSR6vViGXRVxYYeUeYkQOg3vjTF8Csn3VEhCASAcXpd0pSfEDv7PNfbBF7c8Y89GbRG_FZRoJefhkFUyUi105wbPWvgexxBOH76aVPVFer1tjGoSisfEG3D2-41kzFoDcybnmAPVIc)

We will also ensure to use Windows 10 as the operating system, deploying a file we downloaded at the beginning of the project. ![](https://lh3.googleusercontent.com/2ocVrY6u5m5hLaZznoLUwv0S8Ug9Z0xTuLOkU7veuPdo42uAs32GhP1ZWEFqJKaetMZfmjWPWmieW6Vm5goN-GoW8w2g2hb_h-8YDYh6eb1uRaHKieLOwbxi5tGaF-G6DjFwyYTYXkGesTXTy-PEO2E)

10\. Domain Integration and User Authentication:

    - Seamlessly join the secondary VM to the domain, thereby establishing an interconnected environment. Under System Properties, we can join the domain by entering the domain name of the domain controller. 

![](https://lh5.googleusercontent.com/n1mU3uo-8Bt-P38837WSTiChRou5RgIOMplqCyXDs3_J7B_imF939W9rtd0KPweif8jzgQzK9HG2lceLgQKNIn-4z1nAP8GV56BtzjuaylN7_qW8vJBKP34tmooXhK2k1H5ATkNCz4IDGP1g3GjBHzc)

Through the Server Manager on the Domain Controller, we can see a new address lease, confirming that our second virtual machine has connected to the network. ![](https://lh3.googleusercontent.com/guk5jFHhuE13nBByf2A8Am6BissUaA6SuhW5KUTlmZ2f-8BNSHiExwUiCuy3YB07G2P564AT8IkMEVzfXxaQDkLMDRqnzbcuxgW7_V5aya6pxWA5sAHpcukx6skVcO-ETlz6id_EWtGeepwh0lPlOfk)

    - Authenticate a user on the secondary VM utilizing a domain account, showcasing the practical utility of the Active Directory infrastructure. An account generated through the Powershell script can now be used to login to the CLIENT1 virtual machine. This is possible because the second virtual machine was joined to the domain of the Domain Controller. 

**Project Summary**

This project involved the meticulous setup of a simulated corporate network environment using Oracle VirtualBox. Key milestones included configuring a Domain Controller (DC) with Windows Server 2019, establishing Active Directory, implementing Remote Access Service (RAS/NAT) for secure internet access, and deploying a DHCP server for automatic IP assignments. The project culminated with the successful integration of a Windows 10 client VM into the domain, showcasing seamless user authentication and resource access within the interconnected network.
