# Active Directory and DNS - Parent and Child Domains
## INTENTION
For educational purposes showcasing my technical systema and network administrator abilities.
  
## WHAT'S THIS?
Built and configured a logical topology of a multi-city organization featuring Active Directory parent and child domains in VMware Workstation Pro lab environment.
  
## GOALS - Proof Config Implementation Worked Successfully
- CL-SD-01 Win10 VM successfully ping:
    - parent domain `www.CIS.com`
    - public domain `www.google.com`
    - SRV-LA-01.LA.CIS.com
    - SRV-NY-01.NY.CIS.com
- CL-LA-01 Win10 VM successfully ping:
    - parent domain `www.CIS.com`
    - public domain `www.google.com`
    - SRV-SD-01.CIS.com
    - SRV-NY-01.NY.CIS.com
- CL-NY-01 Win10 VM successfully ping:
    - parent domain `www.CIS.com`
    - public domain `www.google.com`
    - SRV-SD-01.CIS.com
    - SRV-LA-01.LA.CIS.com

## TOOLS
- Type 2 hypervisor: VMware Workstation Pro 25H2
  - Device:
    - Windows Server 2022 VM
    - Windows 10 VM
- topology layout and IP labeling: Cisco Packet Tracer 9.0.0
  
## PROTOCOLS IMPLEMENTED - What I Scripted
- Subnet organization, CIS.com, into 3 sites (LA, SD, NY) down to /30 subnets using C class private networks
  - include server network for 1000 host IP addresses
  - include client network for 4000 host IP addresses
- Active Directory
  - Sites (LA, SD, NY)
    - 15 min replication interval
    - SD-LA site link, connecting SD and LA sites
    - SD-NY site link
    - SD-LA-NY site link bridge connecting SD-LA site link and SD-NY site link
  - DNS
  - Web Server
  
## CHALLENGES / LESSON(S) LEARNED
- Challenge: It was a LOT of little configurations to execute, but this was a lot of fun to see it all come together.
- LL: Based on past assignments, I documented my process which is as follows:
  - Phase 1: Initially configure all devices
  - Phase 2: Config static routes and LAN routing
  - Phase 3: Add first set of domain controllers and create domains (CIS.com, Admin.CIS.com, IT.Admin.CIS.com)
  - Phase 4: Add second set of DC's
  - Phase 5: Spot check configs for consistency DNS (Name Servers, Forwarders, Net Adapter DNS IP addresses)
  - Phase 6: Add end host PC's to domains
  - Phase 7: Perform final connectivity tests, snapshots as necessary and screenshot proof of success
- LL: Routers were designated as separate Ethernet ports, while switches became virtual using separate VMnet network adapters
  
## TOPOLOGY
```
 Internet   ➔   SD-FW   ➔   SW-SD-DMZ  ➔   SRV-SD-DMZ

                         ➔     SD-R2    ➔    SW-SD-01   ➔   SRV-SD-01
                                                          ➔   SRV-SD-02
                                         ➔    SW-SD-02   ➔   CL-SD-01

                                         ➔     SD-R1     ➔     LA-R1    ➔   SW-LA-01   ➔   SRV-LA-01
                                                                                          ➔   SRV-LA-02
                                                                          ➔   SW-LA-02   ➔   CL-LA-01

                                                          ➔     NY-R1    ➔   SW-NY-01   ➔   SRV-NY-01
                                                                                          ➔   SRV-NY-02
                                                                          ➔   SW-NY-02   ➔   CL-NY-01

