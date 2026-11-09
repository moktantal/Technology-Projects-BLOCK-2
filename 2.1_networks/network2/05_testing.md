

## 🔍 5. Testing & Verification

### 5.1 Ping Tests  
Did the PC successfully ping a DNS name (e.g., `library_pc1`)?  
Explain the result.
Yes, the PC successfully pinged the DNS name library_pc1. The ping test showed successful replies from the destination PC, which means that the network connection was working correctly. The DNS server successfully translated the hostname library_pc1 into its corresponding IP address. This confirms that both network connectivity and DNS name resolution were working properly.
📸 **Screenshot of successful ping**

<img width="1017" height="695" alt="image" src="https://github.com/user-attachments/assets/aa679df5-afc4-48c3-9d32-6de256316409" />


### 5.2 DNS Resolution  
Describe whether DNS resolved the hostname correctly.

DNS resolved the hostname correctly by translating the computer name library_pc1 into its corresponding IP address. This allowed the PC to communicate with another computer using its hostname instead of typing the IP address manually. The successful DNS resolution shows that the DNS server was configured correctly and working properly.

### 5.3 DHCP Lease Verification  
Describe the IPs assigned to each PC.
The DHCP server automatically assigned IP addresses to each PC on the network. Each PC received a different IP address from the DHCP pool to avoid IP address conflicts.
For example:
PC	Assigned IP address
PC0	192.168.2.10
PC1	192.168.2.11
PC2	192.168.2.12
PC3	192.168.2.13
PC4	192.168.2.14

All PCs use the subnet mask 255.255.255.0.
Do they match the DHCP pool?
"Yes, all five PCs received IP addresses within the configured DHCP pool (192.168.2.100–192.168.2.104). Therefore, the DHCP server is working correctly."

📸 **Screenshot: `ipconfig /all`**
<img width="545" height="497" alt="image" src="https://github.com/user-attachments/assets/e27c04e4-7d1f-46bb-aa1b-7b55866f3faf" />
<img width="570" height="530" alt="image" src="https://github.com/user-attachments/assets/1849ed15-134e-4b0f-bce1-541dac3450d2" />
<img width="1185" height="527" alt="image" src="https://github.com/user-attachments/assets/d3a23ac5-5807-43fd-bafa-f074974c94b0" />




