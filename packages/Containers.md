# All about containers

## What is container and how it is different from VM
### Traditional, before VM
- Unutilized capacity of server
- High cost of servers

| app1 | app2 | app3 |
|-------|------|------|
| server1 | server2 | server3 |
### With VM
| app1 | app2 | app3 |
|-------|------|------|
| os1+kernal | os2+kernal | os3+kernal |
| hipervisor | hipervisor | hipervisor |
| os+kernal | os+kernal | os+kernal |
| server1 | server1 | server1 |
### With Container
| app1 | app2 | app3 |
|-------|------|------|
| container engine | container engine | container engine |
| os+kernal | os+kernal | os+kernal |
| server1 | server1 | server1 |

- if there are security vulnerabilities with the host os+kernal, all container on the host is affected. Compared to this, VMs provide better security as the guest os+kernal provides better security.
- isolation in containers are accomplished via namespaces
- isolation in containers are accomplished via controlgroups
- namespace is a layer of isolation with creates separate enviroments for each container
###
namespace types -
- PID
- Network
- Mount
- user
- UTS

Cgroups - restricts resource usage and monitor how those resources are being utilized

### Comparison between VM and containers
| features/properties | VMs | Containers |
|---------------------|-----|------------|
| isolation           | full isolation from host os and other Vms | lightweight isolation from host os and other containers |
| mutliple apps       | may lead to conflicts, compatibilty issues, & disruptions | each app is packed with its dependencies and isolated from each other |
| emulation           | accomplished by hypervisor | accomplished by container engien |
| cost                | usually high | usually low |
| size                | GBs | MBs |
| start time | minutes | seconds |
| portability/ replaceability | difficult | easy |
| fit for | monolithic application | microservices |

### Monolithilic architecture
| UI |
|----|
| Business Logic |
| Data layer |
| DB |

- advantages - easier to deploy
- disadvantage 
    - all functionality in single code
    - dificult to manage
    - re-depoyment for small change
    - needs downtime

### Microservice architechture
| user interface |
|----------------|
| ms1 ms2 ms3 ms4|
|       DB       |

- advantage
    - each unit is a separate unit
    - better flexibility, scalability, maintanability
    - touch one ms when there is change only to that
- disadvantage
    - complex in terms of architecture
