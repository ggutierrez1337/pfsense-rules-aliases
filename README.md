# Adding Firewall Rules and Aliases with pfSense

# Description
This project documents the addition of firewall rules, positioning of rules on a rule table, along with the creation of aliases. This project assists with securing the internal network ensuring that only traffic allowed by these rules are entering the network and not prohibited IPs or usage of ports. 

## Tools and Utilities
- **VirtualBox**: Used for virtualization of pfSense and Ubuntu.
- **pfSense**: Open-source firewall and router software.
- **Ubuntu Desktop 24**: Interacting with pfSense GUI.

# Documentation

## Adding a New Firewall Rule
When wanting to block something going **out** of the **LAN**, the best interface to set the rule on is the LAN interface

- **Block -** For **external IPs**
- **Reject -** For **internal IPs**

1. In the Web GUI of pfSense, go to **Firewall → Rules**. Select **Add Rule to End of the List**

![image 16](https://github.com/user-attachments/assets/0c9badba-c5b0-430a-9b5f-7a4e74cd1fc6)

2. **Reject** any traffic on port **1337** and give the rule a description

![image 17](https://github.com/user-attachments/assets/a7bf8d28-4c30-4e1f-b1fa-d2ec7b182deb)

![image 18](https://github.com/user-attachments/assets/0ea1d201-3db1-4284-a90e-b0e9fc6f8c3f)

3. Rule order takes precedence and since there is a rule allowing **all** traffic from **any port** to **any port** the rejection of communication on port 1337 will not work. Move the rejection of port 1337 above the **Allow All** rule and now the rule should work
    - Think of the firewall going through each line in the rule table and will stop at the rule that can or may apply to the specific communication and will not traverse the table any further

![image 19](https://github.com/user-attachments/assets/f1a8b66a-10d6-448c-b3c8-8f96e8ea6dcc)

![image 20](https://github.com/user-attachments/assets/ad90d3f9-cc57-4e65-b14a-3a6af71cb161)

## Adding Aliases

Firewall aliases are **named lists of networks, hosts, or ports that can be used in a firewall**. They can be used to make firewall rules shorter, easier to manage, and easier to understand. 

1. Go to **Firewall → Aliases** and select **Add**. Give the Alias a name and select the Port Types and ranges for this Alias to allow out of the LAN

![image 21](https://github.com/user-attachments/assets/d9c256d5-acfd-4151-9851-6af33f4d29b8)

![image 22](https://github.com/user-attachments/assets/f910a16c-44a4-4541-a4ee-e38bb6a90e26)

2. Once the ports have been specified for the aliases, save and apply the changes

![image 23](https://github.com/user-attachments/assets/dde008a4-e3d5-4bc0-8b44-9570583dd5aa)

3. Now that the aliases are made, they need to be applied to the desired firewall rules. Go to **Firewall → Rules → LAN**. Select **Add** and the alias for TCP Ports will be added first
4. Under **Destination** ensure to input the alias name given earlier. This will automatically specify the desired ports
    - e.g. **TCP_Standard_Output**

![image 24](https://github.com/user-attachments/assets/332fb102-7e65-4a82-9bf1-dae8de14c167)

5. Follow the same process for UDP alias and then save all changes

![Screenshot_(1042)](https://github.com/user-attachments/assets/c2a47dce-089f-431e-acdb-5d76f87ec36e)

# Conclusion
By using **Firewall Rules** and **Aliases with pfSense**, the network is more secured allowing only the desired traffic specified in the rule table to be allowed through. By using **Aliases**, rule applying rules is made easier as these aliases specify specific ports and protocols, and they can be used as variables for the application to other rule table. Also, by blocking communication on specific ports, it helps lower the risk of common attacks or known malicious communications from occurring. 
