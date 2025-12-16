
<h1> Security-Operation-Center-SOC-SIEM-lab
</h1>


<h2>Description</h2>
A SOC project was created today using Azure cloud infrastructure. In this project, I created a virtual machine, network security group, SQL database, and a virtual network to catch real-time attackers attacking the virtual website that will be built in the virtual network, also known as a honeypot which the data will be forwarded to logs in a centralized repository.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Virtual Machine</b> 
- <b>Microsoft Sentinel</b>
- <b>KQL</b>
- <b>SQL</b>
- <b>Virtual Network</b>
- <b>Remote Desktop Connection</b>


<h2>Environments Used </h2>

- <b>Windows 11</b>
- <b>Azure</b>
- <b>Microsoft Sentinel</b>
- <b>Command Prompt</b>

<h2>Program walk-through:</h2>

<p align="center">
A SOC project was created today using Azure cloud infrastructure. In this project, I created a virtual machine, network security group, SQL database, and a virtual network to catch real-time attackers attacking the virtual website that will be built in the virtual network, also known as a honeypot which the data will be forwarded to logs in a centralized repository. 
: <br/>
<img src="https://cdn.discordapp.com/attachments/1445251151896248323/1450283247702376500/Screenshot_2025-12-15_181738.png?ex=6941f907&is=6940a787&hm=9460a537b9833354826a4571b7aa28ee3214cc9022d781f09e57e1b4f7006bcd" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
First,  I added a resource group to the subscription that has to be made to use Azure. Resource groups are a logical container used to organize and manage related cloud resources as a single unit. It allows administrators and developers to group services such as virtual machines, databases, storage accounts, and networking components that belong to the same application, project, or environment. By using resource groups, you can apply access controls, policies, and tags consistently across all included resources, making security, governance, and cost management easier:  <br/>
<img src="https://cdn.discordapp.com/attachments/1445251151896248323/1450287844521148488/Screenshot_2025-12-15_184238.png?ex=6941fd4f&is=6940abcf&hm=e15f1ddf16dbb238f549194bcdd3c22b98fef4b2621c8a47c184806113ffc880" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
A virtual network was created and validated inside the resource group: <br/>
<img src="https://cdn.discordapp.com/attachments/1445251151896248323/1450290075014397964/Screenshot_2025-12-15_185332.png?ex=6941ff62&is=6940ade2&hm=31b3fdecd8058774aa6c27359c1fa0d5baa2beee99790c894a30e38607ca768e" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
vritual machine is then created as "AIE-NET-WEST-1":  <br/>
<img src="https://cdn.discordapp.com/attachments/1445251151896248323/1450291367979782214/Screenshot_2025-12-15_183156.png?ex=69420097&is=6940af17&hm=c250a67ecc66928c79c6cec618bbfee638d305b9ca3401f5f73607a5b1d25947&" height="80%" width="80%" alt="Disk Sanitization Steps"/>
 <img src="https://cdn.discordapp.com/attachments/1445251151896248323/1450291368487551209/Screenshot_2025-12-15_183233.png?ex=69420097&is=6940af17&hm=e246d751a7fec1a4579255492309429ca3aa6eaf70ce0422e5f96796aeee9e4a&" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Once the virtual machine was created, I configured the virtual network firewall to be turned off under a new inbound security rule. Destination port ranges will be changed to *, which indicates any range. Priority can be what number is available. I have already made this rule using 100, so here I used 110:  <br/>
<img src="https://cdn.discordapp.com/attachments/1445251151896248323/1450300523789025351/Screenshot_2025-12-15_190057.png?ex=6942091e&is=6940b79e&hm=fd506b94b433e8bb3a7ec7b64f99c727a8bf5757f56a17577718edc1a6ee37c8&" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://cdn.discordapp.com/attachments/1445251151896248323/1450300524351066220/Screenshot_2025-12-15_190316.png?ex=6942091e&is=6940b79e&hm=b74a0382feb54f1cdd6591451c91fe36d1731ac9dd1269d985b3f99a888ece93&" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://cdn.discordapp.com/attachments/1445251151896248323/1450300524858441800/Screenshot_2025-12-15_190601.png?ex=6942091e&is=6940b79e&hm=ed94b7dc35cde93af074b520bbf395428bcc40828c739560ebae2d497c5c8866&" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
After the new inbound rule is configured in the virtual network, use Remote Desktop Connection to access the virtual machine via IP address. When you are in the desktop, go to Windows Defender Firewall properties, turn all tabs off in that window:  <br/>
<img src="https://cdn.discordapp.com/attachments/1445251151896248323/1450303046532993084/Screenshot_2025-12-15_194131.png?ex=69420b77&is=6940b9f7&hm=8f3774a2cec9990741b0d46fda8e7b4b09f7cb5cc778b17b58d699d68f6658b3" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Now test the connection to make sure access is open to you and the public web. Open the command prompt and ping the virtual machine IP address. My subscription is past the 30-day trial period, which means my network is not turned on for my virtual machine, but if this is your first account, then your network should be accessible. You should have more than 0 received packets and less than 50% loss if your virtual network is on:  <br/>
<img src="https://cdn.discordapp.com/attachments/1445251151896248323/1450305633751400601/Screenshot_2025-12-15_195133.png?ex=69420de0&is=6940bc60&hm=742c0e9bb71969e3f8a905237a03a2aa7fbf42f72beacd2cae48763f3b11a6bc" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
Log analytics workspace is created  to collect data entries of potential attacks and will be linked to Microsoft Sentinel (SIEM tool) as a directory:  <br/>
<img src="https://cdn.discordapp.com/attachments/1445251151896248323/1450309681598955633/Screenshot_2025-12-15_200844.png?ex=694211a5&is=6940c025&hm=8b620f3f3b0961fcffed784e8a3b932098697f0c011f6b2e464d20d6d977fc8d&" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://cdn.discordapp.com/attachments/1445251151896248323/1450309682215387166/Screenshot_2025-12-15_201138.png?ex=694211a5&is=6940c025&hm=c778716c3fb87bdf8a40a21dbf86c204ad7ff1e856c58055dfde0f76b2e46487&" height="80%" width="80%" alt="Disk Sanitization Steps"/>"
<br />
<br />
Once in Microsoft Sentinel, create a log space using data from your resource group that has your virtual machine:  <br/>
<img src="https://cdn.discordapp.com/attachments/1445251151896248323/1450314148037791855/Screenshot_2025-12-15_202802.png?ex=694215ce&is=6940c44e&hm=81061fc8e34eddac4e25a9be355bdddb53156c05115863f6234a77a89aa8fefa" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
You can find KQL under the logs tab, where you can search all data within your virtual machine:  <br/>
<img src="https://cdn.discordapp.com/attachments/1445251151896248323/1450315443272286268/Screenshot_2025-12-15_203454.png?ex=69421703&is=6940c583&hm=959e6297c2150f98b135789f2e3b306b700906e64387a0c3daaa31c6a3415d62" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
You will create a workbook with your KQL queries and input them to make a map of all attacks in the world:  <br/>
<img src="https://cdn.discordapp.com/attachments/1445251151896248323/1450316287938134116/Screenshot_2025-12-15_203735.png?ex=694217cc&is=6940c64c&hm=71e7ab441187e201bf1026dc7c86c7b98b25074be2b102487c4edcd983c7b92c" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
I added a map.json code that inputs all queries into a map to make it easier to read and can be used for reports. This is the completed VM attack map worldwide within 24 hours of being open:  <br/>
<img src="https://cdn.discordapp.com/attachments/1445251151896248323/1450321333782319135/Screenshot_2025-12-15_204207.png?ex=69421c7f&is=6940caff&hm=15a3661219c6ebe492691b22c510167c4aacaca6824c86efcf9895911ae9e9cd&" height="80%" width="80%" alt="Disk Sanitization Steps"/>
 <img src="https://cdn.discordapp.com/attachments/1445251151896248323/1450321334373453855/Screenshot_2025-05-13_082456.png?ex=69421c7f&is=6940caff&hm=f2fa49750fa738425192a2bf5a1061889b2cbb29f639e43824904098aeb2e3d4&" height="80%" width="80%" alt="Disk Sanitization Steps"/>
 <img src="https://cdn.discordapp.com/attachments/1445251151896248323/1450321334927233215/Screenshot_2025-05-13_083904.png?ex=69421c7f&is=6940caff&hm=23fde46e25f17e4112d869635f9d5861ad2a0904d37d26f2db585a06e2dc0ba7&" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
