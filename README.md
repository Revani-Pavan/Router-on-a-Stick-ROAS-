# Router-on-a-Stick-ROAS-


Router-on-a-Stick (ROAS) is an inter-VLAN routing method where a single physical router interface connects to a switch as an 802.1Q trunk, and the router uses subinterfaces (one per VLAN) to route traffic between VLANs. Each subinterface acts like a “virtual interface” with its own VLAN tag and IP gateway.

Why use ROAS instead of “regular interfaces”?

If you use regular interfaces (one physical router port per VLAN), you need:

3 VLANs = 3 separate router ports + 3 switch ports

More cables, more physical ports, more hardware dependency

ROAS is used because:

1) Saves router interfaces (1 port can handle many VLANs)

With ROAS:

1 router port + trunk link can route for VLAN10, VLAN20, VLAN30… etc.

2) Cheaper and practical for small/medium networks

You don’t need a multilayer switch; a normal Layer 2 switch + router works.

3) Easier VLAN expansion

Adding a new VLAN is mostly:

create VLAN on switch

add router subinterface + gateway

⚠️ ROAS limitation (important)

All inter-VLAN traffic goes through one physical link, so:

it can become a bottleneck in high-traffic enterprise networks
That’s why large networks often use Layer 3 switches instead.

<img width="1535" height="1183" alt="image" src="https://github.com/user-attachments/assets/1710289e-508d-4021-8e01-d33d155253ff" />

How to do the ROAS Lab (Detailed)

I’ll explain using the same VLANs/subnets from diagram:

VLAN 10 Engineering: 10.0.0.0/26 → gateway will be 10.0.0.62

VLAN 20 HR: 10.0.0.64/26 → gateway will be 10.0.0.126

VLAN 30 Sales: 10.0.0.128/26 → gateway will be 10.0.0.190

Mask for all: 255.255.255.192

Step 1: Assign IPs to PCs

Set each PC IP and gateway:

VLAN 10

PC1: 10.0.0.1 /26 GW 10.0.0.62
<img width="1377" height="1391" alt="image" src="https://github.com/user-attachments/assets/11a9adba-e00b-4d4e-80a1-fd5cfbb4f397" />
<img width="1379" height="1398" alt="image" src="https://github.com/user-attachments/assets/0fb1c229-8b2d-4918-92a7-76bca529395d" />


PC2: 10.0.0.2 /26 GW 10.0.0.62
<img width="1410" height="1419" alt="image" src="https://github.com/user-attachments/assets/55f588f2-7125-4a18-92a5-ed5d37175b48" />
<img width="1379" height="1416" alt="image" src="https://github.com/user-attachments/assets/40825795-2774-4079-8f1f-f1a96829a690" />

PC6: 10.0.0.4 / 26 GW 10.0.0.62
<img width="1388" height="1378" alt="image" src="https://github.com/user-attachments/assets/36394421-1226-4037-acce-5ee48d78eeb0" />
<img width="1357" height="1401" alt="image" src="https://github.com/user-attachments/assets/f3a7cfb2-03bd-4893-af80-021c9d766799" />


PC7: 10.0.0.3 / 26 GW 10.0.0.62
<img width="1391" height="1399" alt="image" src="https://github.com/user-attachments/assets/4f76ee6d-f483-4126-a903-6e23e85ce093" />
<img width="1392" height="1411" alt="image" src="https://github.com/user-attachments/assets/9a85f1db-f408-42e0-9697-b668b559fb04" />


VLAN 20

PC5: 10.0.0.65 /26 GW 10.0.0.126
<img width="1389" height="1392" alt="image" src="https://github.com/user-attachments/assets/21409a37-cf91-4b39-acbb-bef4ef6b0f02" />
<img width="1390" height="1414" alt="image" src="https://github.com/user-attachments/assets/55078c2a-c9ed-49a2-966a-0c1a2112a8bd" />


VLAN 30

PC3: 10.0.0.129 /26 GW 10.0.0.190
<img width="1400" height="1423" alt="image" src="https://github.com/user-attachments/assets/d66e87a9-407b-481f-ba17-e99c8b8130f0" />
<img width="1390" height="1416" alt="image" src="https://github.com/user-attachments/assets/0a2fbcfe-d34e-4f10-8b8d-12abb193fce1" />


Pc4: 10.0.0.130 /26 GW 10.0.0.190
<img width="1378" height="1395" alt="image" src="https://github.com/user-attachments/assets/e90d32f5-648c-4db6-ae24-6754f9310386" />
<img width="1396" height="1409" alt="image" src="https://github.com/user-attachments/assets/2eb83df8-896c-4c31-a2ad-54cc671a1b2c" />

(Packet Tracer: PC → Desktop → IP Configuration)

Step 2: Create VLANs on the Switch while assigning the access port

here we dont create the vlan seperately, when we add a interface to a vlan if it doesnt exist switch will automatically create a vlan.

here we are creating a vlan 10 and also assigning the interface fa0/1,fa0/2 on SW1
<img width="1431" height="523" alt="image" src="https://github.com/user-attachments/assets/375a56c0-aa50-428f-b37c-917fb83e4e95" />

here we are creating a vlan 30 and also assigning the interface fa0/3, fa0/4 on SW1
<img width="1579" height="697" alt="image" src="https://github.com/user-attachments/assets/310299d8-1989-4ff5-becd-76fe626f6141" />

here we are creating a vlan 20 and also assigning the interface fa0/1 on SW2
<img width="1328" height="648" alt="image" src="https://github.com/user-attachments/assets/625c0636-0aa1-4b7d-8ddd-2584b08569f7" />

here we are creating a vlan 10 and also assigning the interface fa0/2, fa0/3 on SW2
<img width="1284" height="1127" alt="image" src="https://github.com/user-attachments/assets/fadc3f73-fae9-4578-bda5-d551b32ebd19" />
making sure that we have created and assigned the vlans as per the diagram (topology) by show vlan brief
<img width="2146" height="574" alt="image" src="https://github.com/user-attachments/assets/d844cb87-8744-48ac-a6c4-1ae34ec5f1f6" />
<img width="2007" height="652" alt="image" src="https://github.com/user-attachments/assets/7dd56ce1-4541-4019-8d9d-c02b822e41b4" />

now we will allow only necessary traffic on that interface and turn the native vlan to any unused vlan
<img width="1253" height="1069" alt="image" src="https://github.com/user-attachments/assets/d4ca9e1d-3802-4038-a882-627930d3736a" />

allowed trunk interfaces and vlans on the switches
<img width="2305" height="594" alt="image" src="https://github.com/user-attachments/assets/e91481e0-f95e-4534-9845-5d5d5e7aa774" />
<img width="2310" height="716" alt="image" src="https://github.com/user-attachments/assets/a3ef8ff5-98b0-48cd-9f0a-6ad5100a886e" />
<img width="2465" height="856" alt="image" src="https://github.com/user-attachments/assets/b9ad537c-bca1-4324-9ba2-22960d16ffca" />
<img width="2075" height="1078" alt="image" src="https://github.com/user-attachments/assets/bee7bc0c-2e3d-402b-89d7-a3a8a491c623" />

switch 1 will not revieve the traffic of vlan 30 bec switch 2 dont alloew the vlan 30 traffic be there no vlan 30 on the switch 2so will create vlaan 30 on SW2
<img width="2074" height="1089" alt="image" src="https://github.com/user-attachments/assets/2921ab0a-fe95-442f-bb06-60d5acb6ee19" />

now you can see that vlan is created and it will allow traffic to vlan 30 through G0/1  an it doesnt need traffic of vlan 20 because there is no device of vlan 20 on the SW1

now we need to allow all the traffic of vlans through SW2 and R1 and set the native vlan to an unsed native vlan
<img width="2044" height="210" alt="image" src="https://github.com/user-attachments/assets/21b3b3c8-63c0-4a4b-a468-f55a0ab28bab" />

 Configure Router Subinterfaces (ROAS)

On the router, you will use ONE physical interface (example: G0/0) and create subinterfaces:

<img width="2117" height="1042" alt="image" src="https://github.com/user-attachments/assets/7f8ff2de-47b3-4b92-bcc7-0a840bea2048" />
we will assign gateway address for the each subinterfaces
<img width="1979" height="550" alt="image" src="https://github.com/user-attachments/assets/56d3a75e-997f-4346-a270-546a75d8c4d4" />
<img width="2100" height="534" alt="image" src="https://github.com/user-attachments/assets/cf334f6e-d1f7-49d1-a48e-0026b0959766" />
<img width="2178" height="577" alt="image" src="https://github.com/user-attachments/assets/9f2cdd00-67b0-4875-b257-45c135c55e4a" />

Verify:

show ip interface brief
<img width="2852" height="654" alt="image" src="https://github.com/user-attachments/assets/e349d563-770e-45f8-9087-5704fcdc9b07" />


Step 6: Test Connectivity
Same VLAN ping:

PC1 → ping PC2 
<img width="1786" height="883" alt="image" src="https://github.com/user-attachments/assets/3576d8b5-b7fb-443c-a8ab-96c9013baa9a" />




Inter-VLAN ping (this proves ROAS works):

PC1 → ping PC3 

<img width="1823" height="1218" alt="image" src="https://github.com/user-attachments/assets/aa437b91-350c-4a96-9a82-d364da4dbf69" />
PC1 → ping PC5 
<img width="1666" height="720" alt="image" src="https://github.com/user-attachments/assets/a2d9dbe8-b22f-4d04-a70c-1e2b31289800" />

PC6 → ping PC2 
<img width="1355" height="1311" alt="image" src="https://github.com/user-attachments/assets/adb46b04-cbc2-48a2-acc1-818f982c54c9" />


