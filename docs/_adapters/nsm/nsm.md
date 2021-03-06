---
layout: page
title: Network Service Mesh Adapter
name: Network Service Mesh
version: v0.2.1
port: 10004/tcp
project_status: stable
github_link: https://github.com/layer5io/meshery-nsm
image: /docs/assets/img/service-meshes/nsm.svg
---

# {{ page.name }}

| Service Mesh   | Adapter Status | Latest Supported Mesh Version |
| :------------: | :------------:   | :------------:              |
| {{page.title}} | <a href ="{{ page.github_link }}" target="_blank">{{ page.project_status }}</a> | {{page.version}}  |

### Lifecycle management of {{ page.name }}

The {{page.name}} can install **{{page.version}}** of the {{page.name}} service mesh. The SMI adapter for Network Service Mesh can also be installed using Meshery.

### Lifecycle management of sample applications

The ({{ page.name }}) includes a handful of sample applications. These applications represent different network services orchestrated by Network Service Mesh. Use Meshery to deploy any of these sample applications:

#### 1. **Hello NSM Application**

Watch this presentation to see the Hello NSM Application in-action:
<iframe class="container" width="370" height="315" src="https://www.youtube.com/embed/4xKixsDTtdM" frameborder="0" allow="accelerometer; autoplay; align="left"; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

See on YouTube: [Adopting Network Service Mesh with Meshery](https://www.youtube.com/watch?v=4xKixsDTtdM&list=PL3A-A6hPO2IOpTbdH89qR-4AE0ON13Zie)

#### 2. **VPP-ICMP Application**

_A simple example that connects a vpp based Pod to a Network Service using memif._

The simplest possible case for Network Service Mesh is to have is connecting a Client via a vWire to another Pod that is providing a Network Service.
Network Service Mesh allows flexibility in the choice of mechanisms used to provide that vWire to a workload.

The icmp responder example does this with kernel interfaces.  The vpp-icmp-responder provides and consumes the same 'icmp-responder' Network Service, but has Client's and Endpoint's that use a [memif](https://www.youtube.com/watch?v=6aVr32WgY0Q) high speed memory interfaces to achieve performance unavailable via kernel interfaces.

![vpp-icmp-responder-example](./vpp-icmp-responder-example.svg)

**Working process**

This will install two Deployments:

Name | Description
:--------|:--------
**vpp-icmp-responder-nsc** | The Clients (four replicas)
**vpp-icmp-responder-nse** | The Endpoints (two replicas)

And cause each Client to get a vWire connecting it to one of the Endpoints.  Network Service Mesh handles the Network Service Discovery and Routing, as well as the vWire 'Connection Handling' for setting all of this up.

![vpp-icmp-responder-example-2](./vpp-icmp-responder-example-2.svg)

In order to make this case more interesting, Endpoint1 and Endpoint2 are deployed on two separate Nodes using PodAntiAffinity, so that the Network Service Mesh has to demonstrate the ability to string vWires between Clients and Endpoints on the same Node and Clients and Endpoints on different Nodes.

**Verification**

First verify that the vpp-icmp-responder example Pods are all up and running:

```bash
kubectl get pods | grep vpp-icmp-responder
```

To see the vpp-icmp-responder example in action, you can run:

```bash
curl -s https://raw.githubusercontent.com/networkservicemesh/networkservicemesh/master/scripts/nsc_ping_all.sh | bash
```

#### 3. **ICMP Responder**

The simplest possible case for Network Service Mesh is to have is connecting a Client via a vWire to another Pod that is providing a Network Service. We call this case the ‘icmp-responder’ example, because it allows the client to ping the IP address of the Endpoint over the vWire.

![icmp-responder-example](./icmp-responder-example.svg)

**Outcomes**

This will install two Deployments:

Name | Description |
:--------|:--------
**icmp-responder-nsc** | The Clients, four replicas |
**icmp-responder-nse** | The Endpoints, two replicas |

And cause each Client to get a vWire connecting it to one of the Endpoints.  Network Service Mesh handles the
Network Service Discovery and Routing, as well as the vWire 'Connection Handling' for setting all of this up.

![icmp-responder-example-2](./icmp-responder-example-2.svg)

In order to make this case more interesting, Endpoint1 and Endpoint2 are deployed on two separate Nodes using
`PodAntiAffinity`, so that the Network Service Mesh has to demonstrate the ability to string vWires between Clients and
Endpoints on the same Node and Clients and Endpoints on different Nodes.

**Verification**

1. Verify that the icmp-responder example Pods are all up and running:

```bash
kubectl get pods | grep icmp-responder
```

2. To see the icmp-responder example in action, you may run:

```bash
curl -s https://raw.githubusercontent.com/networkservicemesh/networkservicemesh/master/scripts/nsc_ping_all.sh | bash
```

### Suggested Topics

- Examine [Meshery's architecture]({{ site.baseurl }}/architecture) and how adapters fit in as a component.
- Learn more about [Meshery Adapters]({{ site.baseurl }}/architecture/adapters).
