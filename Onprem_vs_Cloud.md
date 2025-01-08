# On-Prem vs Cloud Service Support in N-Central:

| S.No | On-Prem Supported Devices | Cloud Supported Services |
| ---- | ------------------------- | ------------------------ |
| 1 | Physical Devices: Desktops, Laptops, Servers | Virtual Machines in IaaS environments (e.g., Azure VMs, AWS EC2) |
| 2 | Platforms: Linux, Windows, macOS | Platforms: Linux, Windows |
| 3 | Network Devices: Switches, Routers, Firewalls (with SNMP enabled for monitoring) | Networking in PaaS services: Managed by the cloud provider with limited control over hardware and OS functionality |
| 4 | No PaaS concept in on-premises environments | Cloud-native PaaS services: Not directly supported for monitoring due to lack of agent installation capabilities |
| 5 | Extensive monitoring: Supported via SNMP, agents, or custom scripts | Monitoring: Limited to services with agent support or third-party integrations |

**Note:**
The N-able N-central REST API primarily facilitates interactions with devices and services that have agents installed, typically within IaaS environments. Since PaaS services in Azure do not provide OS-level access for agent installation, direct monitoring via N-central's REST API is not feasible.

## Alternatives for Monitoring Azure PaaS Services:

**Native Azure Monitoring Tools:**
Utilize Azure Monitor and Log Analytics to collect and analyze metrics and logs from the PaaS resources. While this provides robust monitoring, it lacks integration into N-central’s single-dashboard view.

**ITSM Integration:**
Use ITSM tools to integrate health alerts into platforms like HaloPSA. This allows for centralized incident management but still relies on Azure's native tools for detailed insights.

**N-central Probe Application:**
For IaaS (VMs), a Windows Server is required to install the probe application, which incurs additional costs. This approach is better suited for IaaS environments rather than PaaS.

**Recommendation:**
For monitoring both IaaS and PaaS environments, leveraging Azure’s native tools combined with ITSM integration is a cost-effective and efficient solution. However, for more advanced integrations or specific requirements, consider consulting N-able’s support team to explore additional options.