---

copyright:
  years: 2026
lastupdated: "2026-12-26"

keywords:

subcollection: pattern-transit-vpc-fortigate

---

{{site.data.keyword.attribute-definition-list}}

# Overview
{: #overview}

This deployment guide provides a specific implementation scenario for securing multiple landing zones using a transit IBM Cloud VPC architecture with FortiGate firewalls on IBM Cloud.
Building upon the foundational concepts presented in the [Securing multiple landing zones with a transit VPC and advanced security capabilities](https://cloud.ibm.com/docs/pattern-transit-vpc?topic=pattern-transit-vpc-transit-vpc) whitepaper, this guide demonstrates a practical deployment using FortiGate Next-Generation Firewalls (NGFW) as the security appliance within the transit IBM Cloud VPC.
In this version of the architecture, the FortiGate appliances are deployed using the multi-zone region (MZR) Cross-Zone High Availability (HA) offering, which distributes the firewall instances across multiple availability zones to improve resiliency and fault tolerance. This deployment leverages the IBM Cloud catalog offering for Fortinet FortiGate Cross-Zone HA, enabling automated provisioning via Terraform and providing built-in support for high availability, VPN, and advanced security services.
The guide covers the complete architecture design, detailed deployment steps, and configuration procedures for implementing high-availability FortiGate clusters to inspect and control traffic flows between landing zones, on-premises networks, and the internet, providing enterprise-grade security and network segmentation for multi-tenant cloud environments.
