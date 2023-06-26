# Virtual Machine

## Sources
- https://www.youtube.com/watch?v=iUaTq06m26g&list=PLGjZwEtPN7j9tM6QHM9XbuHhkE_81i439&index=2&ab_channel=AdamMarczak-AzureforEveryone

- Virtual Machines are the classical example of Infrastructure as Code

## Components of a Virtual Machine
- Virtual Machine
    - Logical resource to manage the ther VM componentes
    - Allows scaling up and down, in and out
    - Configuring extensions
    - Adding/removing disks
- Disks
    - OS Disk
        - Managed disk
        - Used for the system installation
        - Contains the boot volume
    - Temporary Disk
        - Isn't managed
        - Short-term storage for application data
        - Data isn't guaranteed to be kept during maintenance
        - SSD
        - Included in the VM's pricing
    - Data disks
        - Managed disks
        - Used for application data
        - Come in several shapes and sizes
- Network Interface (NIC)
    - Attaches to a virtual network's subnet and connects the VM to it
    - Minimum of 1 per VM
    - Has an assigned MAC address
    - Has a private IP for internal connections
- Network Security Group
  - Filters inbound and outbound traffic to the VM
- Diagnostic Storage
  - Stores boot and OS diagnostic logs

## Key Features
- Both Windows and Linux
- Options for extensions and automation
- Creating custom images
- High availability
- Monitoring
- Availability sets, availability zones and scale sets

## Scale Sets
- Group of identical VMs using the same Image
- Also creates a load balancer to control traffic to VMs
- Number of VMs scale based on scheduled or demand, defined by auto-scaler rules

## Availability Sets
- Fault Domain: Group of VMs that share a common power source and network switch
- Update Domain: Group of VMs that can be restarted at the same time for updates
- Azure will distribute all machines in the availability sets accross several fault and update domains

## Availability Zones
- Group of servers that has its own cooling, power and networking within an Azure region
- Protect VMs from data center outages

## Typical VM scenarios
- On premises gateway services
- Bastion hosts (jumpbox)
- High performance comupting
- Batch jobs
- Cluster solutions
- Lift-n-shift scenarios
- For services unavailable in Azure as PaaS

---

# Demos
- [ ] Creating a VM
- [ ] Connecting via RDP
- [ ] Creating with Azure CLI
- [ ] Connecting via SSH
- [ ] Setting up Extensions
- [ ] Managing NSG
- [ ] Managing Disks

## Creating with Azure CLI
```
az vm create \
    --name my-virtual-machine \
    --resource-group vm-RG \
    --admin-username bernardino \
    --generate-ssh-keys \
    --image UbuntuLTS
    --location westus2
```

**Checkpoint:** 17:30