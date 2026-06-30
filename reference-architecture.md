---

copyright:
  years: 2026
lastupdated: "2026-06-30"

keywords:

subcollection: pattern-transit-vpc-fortigate-multizone

---

{{site.data.keyword.attribute-definition-list}}

# Architecture
{: #architecture}

For this deployment guide, we created the following extensive test environment to simulate traffic flow for each of our connectivity use cases. Here is a diagram:

![Image 1](images/image-01.svg){: caption="Image 1" caption-side="bottom"}

## Architecture details:
{: #architecture details}

* Transit VPC

    The pair of FortiGate firewalls has been deployed in the transit VPC in a high-availability configuration to ensure continuous traffic inspection. Two instances provide redundancy and enable failover in case of failure.
    The FortiGate appliances are deployed across two availability zones within a multi-zone region (MZR) using a cross-zone HA design (Active-Passive), improving resiliency against zone failures. All route tables use the FortiGate instances as the next hop, ensuring traffic is consistently inspected.

* Two spoke VPCs with two test VSIs in each of them, one in each zone

    "Spokes TGW" the Transit Gateway used to connect the Spoke VPCs to the transit VPC

* External Access (North/South):

    - Direct Link: *In order to simulate an on-prem network, a PowerVS workspace in Chennai was used; this PowerVS is connected to the Transit VPC via a Direct Link Connect. However, this architecture is flexible enough to use any on-prem to IBM Cloud topology a Direct Link connectivity*.
        - The Direct Link was terminated directly in the transit VPC (no Transit Gateway), this allows traffic control with an ingress route table that is separate from the Transit Gateway ingress route table.
        - A Linux based PowerVS instance was deployed to test traffic.

    - VPN: The external VPN connectivity for management access was simulated using a S2S VPN Gateway installed in an "onprem-mgmt" VPC.
        - A S2S VPN gateway was installed in a "mgmt-vpn" VPC to simulate the cloud-based VPN endpoint that the "on-premise" VPN connects to.
        - These two VPCs were only connected with each other over the public Internet using the S2S VPN connection (no Transit Gateway connections between these VPCs)
        - "TGW Mgmt VPN" that was created to connect the management VPC and VPN connection to the Transit VPC
        - We utilised the new "dynamic route" based VPN connection type that uses BGP based connectivity (GRE tunnels) into the Transit Gateway

* Public Access: An external system was used to test public connectivity over the Internet (laptop without VPN). Public address ranges (PARs) were used in the transit VPC to provide the firewall with public IP connectivity.

* Internal access
   - Spoke to spoke (East/West): Traffic test included traffic between spokes that is forced through the firewall for inspection
   - Management to spokes: All traffic from the management VPC traversed the firewall
