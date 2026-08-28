---
title: Currently Used Terminology Related to Source Address Validation
abbrev: SAV Terminology
docname: draft-gq-savnet-sav-terms-02
obsoletes:
updates:
date:
category: info
submissionType: IETF

ipr: trust200902
area: Routing
workgroup: SAVNET
keyword: Internet-Draft

author:
 -
  ins: N. Geng
  name: Nan Geng
  organization: Huawei
  email: gengnan@huawei.com
  city: Beijing
  country: China
 -
  ins: L. Qin
  name: Lancheng Qin
  organization: Zhongguancun Laboratory
  email: qinlc@zgclab.edu.cn
  city: Beijing
  country: China

# normative:

informative:
  RFC1195:
  RFC2328:
  RFC2827:
  RFC3222:
  RFC3704:
  RFC4271:
  RFC4364:
  RFC5210:
  RFC5340:
  RFC6480:
  RFC6793:
  RFC8704:
  RFC9234:
  RFC9582:
  I-D.ietf-savnet-intra-domain-problem-statement:
  I-D.ietf-savnet-inter-domain-problem-statement:
  I-D.ietf-savnet-intra-domain-architecture:
  I-D.ietf-savnet-inter-domain-architecture:
  I-D.ietf-savnet-general-sav-capabilities:
  I-D.ietf-sidrops-aspa-profile:
  I-D.geng-idr-bgp-savnet:
  I-D.li-sidrops-bicone-sav:
  I-D.ietf-sidrops-bar-sav:
  caida-asrank:
    title: CAIDA AS Rank
    author: 
    org: CAIDA
    date: 2025-08
    target: https://asrank.caida.org/about
  manrs-blog:
    title: Why is Source Address Validation Still a Problem?
    author: 
    org: MANRS
    date: 2023-04
    target: https://manrs.org/2023/04/why-is-source-address-validation-still-a-problem
  savnet-charter:
    title: Charter for SAVNET Working Group
    author:
    org: IETF
    date: 2023-03
    target: https://datatracker.ietf.org/wg/savnet/about

...

--- abstract

This document provides an overview of terms and abbreviations related to Source Address Validation (SAV). Its purpose is to establish a common and consistent set of terminology for use across SAV-related discussions and documents. This document explicitly does not serve as an authoritative source of correct terminology. 

--- middle

# Introduction {#sec-intro}

This document provides an overview of terms and abbreviations related to Source Address Validation (SAV). Its purpose is to establish a common and consistent set of terminology for use across SAV-related discussions and documents. This document explicitly does not serve as an authoritative source of correct terminology. 

## Requirements Language

{::boilerplate bcp14-tagged}

# General Terms

## Network and Topology Terms
- **Autonomous System (AS):** A set of routers under a single technical administration [RFC4271].

- **AS Number (ASN):** A 16-bit [RFC4271] or 32-bit [RFC6793] number uniquely identifying an Autonomous System.

- **Provider (aka Provider AS):** The provider in a customer-to-provider relationship (if looked at from the opposite direction, provider-to-customer {{caida-asrank}}). A Provider may propagate any available route to a Customer [RFC9234]. 

- **Customer (aka Customer AS):** The customer in a customer-to-provider relationship. A Customer may propagate any route learned from a Customer, or that is locally originated, to a Provider. All other routes must not be propagated [RFC9234].

- **Peer (aka Peer AS or Lateral Peer or Lateral Peer AS):** The peers in a lateral peering relationship. A Peer may propagate any route learned from a Customer, or that is locally originated, to a Peer. All other routes must not be propagated [RFC9234].

- **Customer Cone (CC):** The Customer Cone of a given AS, denoted as AS-A, includes: (1) AS-A itself, (2) AS-A's direct customers (ASes), (3) The customers of AS-A's direct customers (indirect customers), (4) And so on, recursively, following all chains of provider-to-customer (P2C) links down the hierarchy {{I-D.ietf-savnet-inter-domain-problem-statement}}{{caida-asrank}}.

- **Provider Cone:** The set of ASes that an AS can reach by using only customer-to-provider links {{I-D.li-sidrops-bicone-sav}}.

## Router and Interface Terms

- **Edge Router:** The router that is directly connected to a Sub Network or a host {{I-D.geng-idr-bgp-savnet}}. 

- **AS Border Router (ASBR):** The router that connects an AS to other ASes. 

- **Internal Router:** The router that is neither an edge router nor a border router in an AS. 

- **Customer Interface (aka Customer-facing Interface):** The interface of an ASBR facing a Customer [RFC8704]. 

- **Lateral Peer Interface (aka Lateral Peer-facing Interface):** The interface of an ASBR facing a Lateral Peer [RFC8704]. 

- **Provider Interface (aka Provider-facing Interface):** The interface of an ASBR facing a Provider [RFC8704]. 

## Routing Terms

- **Interior Gateway Protocol (IGP):** A type of routing protocol used within a single AS to exchange routing information between routers.

- **Intermediate System to Intermediate System (IS-IS):** A link-state routing protocol belonging to IGP and designed to dynamically exchange routing information within a single AS [RFC1195].

- **Open Shortest Path First (OSPF):** Another link-state routing protocol belonging to IGP and designed to dynamically exchange routing information within a single AS {{RFC2328}}{{RFC5340}}.

- **Border Gateway Protocol (BGP):** A path-vector routing protocol used in the global Internet to exchange routing information between different ASes [RFC4271].

- **Routing Information Base (RIB):** A database within a router or network host that stores routing information. RIB is also known as routing table. 

- **Forwarding Information Base (FIB):** The table containing the information necessary to forward IP Datagrams [RFC3222]. FIB is also known as forwarding table. FIB stores the best active routes, which are a subset of those found in the RIB. 

- **Virtual Routing and Forwarding (VRF):** The routing (or forwarding) tables separate from the global routing (or forwarding) table in a router {{RFC4364}}{{RFC8704}}. 

- **Asymmetric Routing:** Asymmetric routing means a packet traverses from a source to a destination in one path and takes a different path when it returns to the source. Asymmetric routing can occur within an AS due to routing policy, traffic engineering, etc {{I-D.ietf-savnet-intra-domain-problem-statement}}. 

## Routing Security Terms

- **Resource Public Key infrastructure (RPKI):** A specialized public key infrastructure (PKI) framework to support improved security for the Internet's BGP routing infrastructure [RFC6480].

- **Route Origin Authorization (ROA):** A digitally signed object in the RPKI that provides a means of verifying that an IP address block holder has authorized an AS to originate routes to one or more prefixes within the address block [RFC9582]. 

- **Autonomous System Provider Authorization (ASPA):** A digitally signed object in the RPKI, that authorizes one or more other ASes as its upstream providers {{I-D.ietf-sidrops-aspa-profile}}. 

- **Internet Routing Registry (IRR):** A public database which allows Internet service providers to publish and look up Internet number bindings and policy objectives.

- **Resource holder:**  A legitimate holder of either IP address or AS number resources [RFC6480].

## Scenario Terms

- **Direct Server Return (DSR):** A traffic delivery model commonly used by Content Delivery Networks (CDNs) that use anycast service addresses while delivering data from edge locations that do not announce those addresses. In such deployments, a request is received by the anycast server, but the response is sent directly by another server (i.e., the edge server) with the anycast service address as the source address, rather than the address used to reach the edge server. This can create a legitimate hidden-prefix scenario. {{I-D.ietf-savnet-intra-domain-problem-statement}}{{I-D.ietf-savnet-inter-domain-problem-statement}}. 

# SAV Terms

## General SAV Terms

- **Source Address Spoofing (aka Source Address Forgery):** The act of using spoofed source IP addresses assigned to other machines. Malicious actors use IP spoofing to invoke a variety of attacks, including Distributed Denial of Service (DDoS) attacks, policy evasion, and a range of application-level attacks {{manrs-blog}}. A spoofed source address can be either IPv4 or IPv6. 

- **Source Address Validation (SAV):** A kind of techniques for the detection and mitigation of Source Address Spoofing [RFC8704]. Routers conduct SAV on data packet in the data plane. SAV focuses on the scenarios of native IP forwarding or IP-encapsulated tunnel (IPsec, GRE, SRv6, etc.). Note that, the SAV mechanisms that the SAVNET working group is interested in should not modify data plane packets {{savnet-charter}}.

- **SAV Rule:** The rule that indicates the validity of a specific source IP address or source IP prefix per router interface. It is used by a router to make SAV decisions {{I-D.ietf-savnet-intra-domain-problem-statement}}.

- **SAV Table:** The table of prefixes that indicates the validity of a specific source IP address or source IP prefix per interface. Sometimes the terms 'RPF (Reverse Path Forwarding) list' or 'SAV rules' are used interchangeably with 'SAV table' {{I-D.ietf-savnet-inter-domain-problem-statement}}.

- **Access Network SAV:** It prevents a host in a network from spoofing the address of another host in the same network segment. Access Network SAV enables source address-granularity of protection [RFC5210].

- **Intra-domain SAV (aka Intra-AS SAV):** The AS validates the source addresses of data traffic that it originates directly or indirectly. Intra-domain SAV is applied at external interfaces (on routers) facing entities that are not deployed as neighboring ASes and are therefore not covered by inter-domain SAV. For example, an entity can be a single host, a set of hosts, or a customer network with no AS that manages one or more IP prefixes. The entity may source traffic using prefixes assigned by the AS or its own BYOIP prefixes. From the perspective of other ASes, such traffic is originated by the AS. {{I-D.ietf-savnet-intra-domain-problem-statement}}

- **Inter-domain SAV (aka Inter-AS SAV):** Inter-domain SAV, defined in the context of Internet routing using BGP-4 [RFC4271], checks the source addresses of data traffic received from a neighboring Autonomous System (AS), whether that traffic originated within the neighbor's network or is being transited through it. Inter-domain SAV is applied at border routers to incoming traffic on external interfaces directly connected to a neighboring AS. The local AS (SAV performing AS) and the neighbor AS are connected using external BGP (eBGP). The neighbor AS could be using either a public AS number (ASN) or a private ASN [RFC6996]. {{I-D.ietf-savnet-inter-domain-problem-statement}}

- **Source Address Validation Architecture (SAVA):** A multiple-fence architecture that takes Access Network SAV, Intra-AS SAV, and inter-AS SAV [RFC5210]. The assumption here is that when access-network SAV is not universally deployed, Intra-AS SAV and Inter-AS SAV can increase the defense in depth by blocking spoofing packets that have entered the network. 

- **Source Address Validation in Intra-domain and Inter-domain Networks (SAVNET):** It refers to both Intra-domain SAV and Inter-domain SAV. The SAVNET working group was created for the evolvement of SAVNET mechanisms {{savnet-charter}}. 

## SAV Enforcement Terms

- **Validation Mode:** The mode indicates how SAV Rules are logically organized and used to conduct validation {{I-D.ietf-savnet-general-sav-capabilities}}.

- **Interface-based Source Prefix Allowlist (aka Source Prefix Allowlist):** A Validation Mode that takes effect on a specific interface. The interface enabling this mode maintains a source prefix list. Only the source addresses encompassed by the source prefixes recorded in the list will be considered valid, otherwise invalid {{I-D.ietf-savnet-general-sav-capabilities}}.

- **Interface-based Source Prefix Blocklist (aka Source Prefix Blocklist):** A Validation Mode that takes effect on a specific interface. The interface enabling this mode maintains a source prefix list. Any source addresses encompassed by the source prefixes recorded in the list will be considered invalid, otherwise valid {{I-D.ietf-savnet-general-sav-capabilities}}.

- **Source Prefix-based Interface Allowlist:** A Validation Mode that takes effect at the router scale. The router enabling this mode will record the source prefixes attached with an interface allowlist. For the packet whose source address is encompassed by a recorded source prefix, the packet is considered valid only when its incoming interface is included in the corresponding interface allowlist. Otherwise, the packet is considered invalid. For the packet whose source address is encompassed by no recorded source prefix, the validity of the packet is unknown {{I-D.ietf-savnet-general-sav-capabilities}}. 

- **Source Prefix-based Interface Blocklist:** A Validation Mode that takes effect at the router scale. The router enabling this mode will record the source prefixes attached with an interface blocklist. For the packet whose source address is encompassed by a recorded source prefix, the packet is considered valid only when its incoming interface is not included in the corresponding interface allowlist. Otherwise, the packet is considered invalid. For the packet whose source address is encompassed by no recorded source prefix, the validity of the packet is unknown {{I-D.ietf-savnet-general-sav-capabilities}}. 

- **Improper Block (aka False Positive):** The validation results in packets with legitimate source addresses being blocked improperly due to inaccurate SAV rules. (The terms 'improper block' and 'false positive' are used synonymously.) {{I-D.ietf-savnet-intra-domain-problem-statement}}{{I-D.ietf-savnet-inter-domain-problem-statement}}.

- **Improper Permit (aka False Negative):** The validation results in packets with spoofed source addresses being permitted improperly due to inaccurate SAV rules. (The terms 'improper permit' and 'false negative' are used synonymously.) {{I-D.ietf-savnet-intra-domain-problem-statement}}{{I-D.ietf-savnet-inter-domain-problem-statement}}.

- **Traffic Handling Policy:** The data plane action taken on the incoming packet after the SAV process on the packet. Besides "Discard", many other actions such as "Permit", "Rate Limit", and "Traffic Redirect" can be chosen and taken for the packet with the invalid state {{I-D.ietf-savnet-general-sav-capabilities}}.

## SAV Mechanism Terms

- **Access Control List (ACL) for SAV:** A filter that checks the source address of a data packet against a list of acceptable or unacceptable prefixes [RFC2827].

- **Strict unicast Reverse Path Forwarding (uRPF):** A mechanism that uses FIB for SAV. An ingress packet is accepted only if the FIB contains a prefix that encompasses the source address and forwarding information for that prefix points back to the interface over which the packet was received {{RFC3704}}. 

- **Feasible-Path uRPF (FP-uRPF):** An extension of Strict uRPF. Instead of just inserting one best route there, the alternative paths (if any) have been added as well, and are valid for consideration {{RFC3704}}. 

- **Loose uRPF:** A mechanism checks only for the existence of a route (even a default route, if applicable), not where the route points to (At least some implementations of Loose uRPF check where the default route points to) [RFC3704].

- **Loose uRPF Ignoring Default Route:** Loose uRPF checks only for the existence of a explicit route (default routes are excluded) [RFC3704].

- **VRF uRPF:** A mechanism that takes SAV based on VRF table instead of FIB. The specific routes received from external BGP peers will be stored in a dedicated VRF table. VRF uRPF can be implemented to support the strict mode like Strict uRPF or the loose mode like Loose uRPF [RFC8704]. 

- **Enhanced Feasible-Path uRPF (EFP-uRPF):** A mechanism that is more flexible about directionality than the FP-uRPF and is for enhancing FP-uRPF in some cases. It is based on the principle that if BGP updates for multiple prefixes with the same origin AS were received on different interfaces (at border routers), then incoming data packets with source addresses in any of those prefixes should be accepted on any of those interfaces [RFC8704]. 

- **BAR-SAV:** A mechanism that generates source prefix allowlists by using BGP UPDATE messages, ASPA, and ROA {{I-D.ietf-sidrops-bar-sav}}. 

- **General SAV Information:** The information that is not specialized for SAV but can be utilized to generate SAV rules, and is initially utilized for other purposes. Currently, the General SAV Information consists of the information from RPKI ROA objects and ASPA objects, local routing information, and the information from IRR data {{I-D.ietf-savnet-inter-domain-architecture}}.

- **SAV-related Information:** Routing information (e.g., RIBs and FIBs populated by routing protocols or by the local configuration information -- described below -- provided by the AS operator) and objects published in the Resource Public Key Infrastructure (RPKI) that were originally proposed for non-SAV purposes but may also be used for SAV. The RPKI objects include existing RPKI object types (e.g., ROAs and ASPAs) as well as any new types that may be proposed. {{I-D.ietf-savnet-inter-domain-problem-statement}}

- **SAV-specific Information:** Information dedicated to SAV, which may be defined and exchanged between ASes using potentially new inter-AS communication protocol or an extension of an existing protocol. The information may also take the form of new RPKI object type(s). It may also come from the local configuration information provided by the AS operator. {{I-D.ietf-savnet-inter-domain-problem-statement}}

- **Configuration Information:** This information is configured locally by the AS operator. For example, an AS provisions (suballocates) prefixes p1 and p2 for a non-BGP customer network, which also owns an RIR-allocated prefix p3. The customer instructs the AS to advertise p1 via eBGP on the public Internet, restrict p2 strictly to internal use (in the customer network), and refrain from advertising p3 while still allowing it to source outbound traffic. The AS locally configures these prefixes accordingly. This configuration information is valuable for both intra-domain SAV to permit expected prefixes and inter-domain SAV at other interfaces to block unexpected prefixes. {{I-D.ietf-savnet-inter-domain-problem-statement}}

- **Source Entity (aka Source Router or Source AS):** The Entity (Router/AS) that propagates its SAV-specific information to Validation Entity (Router/AS) {{I-D.ietf-savnet-intra-domain-architecture}}{{I-D.ietf-savnet-inter-domain-architecture}}. Source Entity is the producer of SAV-specific information. 

- **Validation Entity (aka Validation Router or Validation AS):** The Entity (Router/AS) that receives SAV-specific information from Source Entity (Router/AS) {{I-D.ietf-savnet-intra-domain-architecture}}{{I-D.ietf-savnet-inter-domain-architecture}}. Validation Entity is the consumer of SAV-specific information. 

# Security Considerations {#sec-security}

This document provides an overview of terms and abbreviations related to SAV and does not have security considerations.

# IANA Considerations {#sec-iana}

There is no IANA requirement.

--- back


