---
title: Currently Used Terminology Related to Source Address Validation
abbrev: SAV Terminology
docname: draft-gq-savnet-sav-terms-00
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

- **Sub Network:** A sub network may operate its own internal routing protocols, but it is considered part of the AS in the global routing system. It is connected to one or more routers of the AS for Internet connectivity. It originates traffic but does not transit traffic for other networks {{I-D.ietf-savnet-intra-domain-problem-statement}}. 

- **Provider (aka Provider AS):** The provider in a customer-to-provider relationship (if looked at from the opposite direction, provider-to-customer {{caida-asrank}}). A Provider may propagate any available route to a Customer [RFC9234]. 

- **Customer (aka Customer AS):** The customer in a customer-to-provider relationship. A Customer may propagate any route learned from a Customer, or that is locally originated, to a Provider. All other routes must not be propagated [RFC9234].

- **Peer (aka Peer AS or Lateral Peer or Lateral Peer AS):** The peers in a lateral peering relationship. A Peer may propagate any route learned from a Customer, or that is locally originated, to a Peer. All other routes must not be propagated [RFC9234].

- **Customer Cone:** The set of ASes that an AS can reach by using only provider-to-customer links {{caida-asrank}}.

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

## Others

- **Direct Server Return (DSR):** A Content Delivery Network (CDN) technique. The anycast server receives requests from users and creates tunnels to the edge server, and the edge server directly sends the requested content to users. The source address of the response packets is the anycast IP address of the anycast server, but the network hosting the edge server does not announce the anycast address in BGP {{I-D.ietf-savnet-inter-domain-problem-statement}}. 

# SAV Terms

## General SAV Terms

- **Source Address Spoofing (aka Source Address Forgery):** The act of using spoofed source IP addresses assigned to other machines. Malicious actors use IP spoofing to invoke a variety of attacks, including Distributed Denial of Service (DDoS) attacks, policy evasion, and a range of application-level attacks {{manrs-blog}}. A spoofed source address can be either IPv4 or IPv6. 

- **Source Address Validation (SAV):** A kind of techniques for the detection and mitigation of Source Address Spoofing [RFC8704]. Routers conduct SAV on data packet in the data plane. SAV focuses on the scenarios of native IP forwarding or IP-encapsulated tunnel (IPsec, GRE, SRv6, etc.). Note that, the SAV mechanisms that the SAVNET working group is interested in should not modify data plane packets {{savnet-charter}}.

- **SAV Rule:** The rule that describes the binding relationship between a source address (prefix) and a valid/invalid incoming interface(s) {{I-D.ietf-savnet-intra-domain-problem-statement}}. SAV Rules can be used for validating whether a data packet with a source address arrive at the router (enforing SAV based on SAV Rules) from an expected interface, and thus determining whether the source address is spoofed (i.e., valid) or not (i.e., invalid). 

- **SAV Table:** The table or data structure that implements the SAV rules and is used for performing source address validation in the data plane {{I-D.ietf-savnet-inter-domain-architecture}}.

- **Access Network SAV:** It prevents a host in a network from spoofing the address of another host in the same network segment. Access Network SAV enables source address-granularity of protection [RFC5210].

- **Intra-domain SAV (aka Intra-AS SAV):** It prevents a Sub Network from using a source address out of the Sub Network or prevents a host from using a source address out of the network segment. Intra-domain SAV mostly enables source prefix-granularity of protection. 

- **Inter-domain SAV (aka Inter-AS SAV):** It prevents Source Address Spoofing packets across ASes. Inter-domain SAV mostly enables source prefix-granularity of protection. 

- **Source Address Validation Architecture (SAVA):** A multiple-fence architecture that takes Access Network SAV, Intra-AS SAV, and inter-AS SAV [RFC5210]. The assumption here is that when access-network SAV is not universally deployed, Intra-AS SAV and Inter-AS SAV can increase the defense in depth by blocking spoofing packets that have entered the network. 

- **Source Address Validation in Intra-domain and Inter-domain Networks (SAVNET):** It refers to both Intra-domain SAV and Inter-domain SAV. The SAVNET working group was created for the evolvement of SAVNET mechanisms {{savnet-charter}}. 

## SAV Enforcement Terms

- **Validation Mode:** The mode indicates how SAV Rules are logically organized and used to conduct validation {{I-D.ietf-savnet-general-sav-capabilities}}.

- **Interface-based Source Prefix Allowlist (aka Source Prefix Allowlist):** A Validation Mode that takes effect on a specific interface. The interface enabling this mode maintains a source prefix list. Only the source addresses encompassed by the source prefixes recorded in the list will be considered valid, otherwise invalid {{I-D.ietf-savnet-general-sav-capabilities}}.

- **Interface-based Source Prefix Blocklist (aka Source Prefix Blocklist):** A Validation Mode that takes effect on a specific interface. The interface enabling this mode maintains a source prefix list. Any source addresses encompassed by the source prefixes recorded in the list will be considered invalid, otherwise valid {{I-D.ietf-savnet-general-sav-capabilities}}.

- **Source Prefix-based Interface Allowlist:** A Validation Mode that takes effect at the router scale. The router enabling this mode will record the source prefixes attached with an interface allowlist. For the packet whose source address is encompassed by a recorded source prefix, the packet is considered valid only when its incoming interface is included in the corresponding interface allowlist. Otherwise, the packet is considered invalid. For the packet whose source address is encompassed by no recorded source prefix, the validity of the packet is unknown {{I-D.ietf-savnet-general-sav-capabilities}}. 

- **Source Prefix-based Interface Blocklist:** A Validation Mode that takes effect at the router scale. The router enabling this mode will record the source prefixes attached with an interface blocklist. For the packet whose source address is encompassed by a recorded source prefix, the packet is considered valid only when its incoming interface is not included in the corresponding interface allowlist. Otherwise, the packet is considered invalid. For the packet whose source address is encompassed by no recorded source prefix, the validity of the packet is unknown {{I-D.ietf-savnet-general-sav-capabilities}}. 

- **Improper Block (aka False Positive):** The problem that the packets with legitimate source addresses are improperly considered invalid due to inaccurate SAV Rules {{I-D.ietf-savnet-intra-domain-problem-statement}}{{I-D.ietf-savnet-inter-domain-problem-statement}}.

- **Improper Permit (aka False Negative):** The problem that the packets with spoofed source addresses are improperly considered valid due to inaccurate SAV Rules {{I-D.ietf-savnet-intra-domain-problem-statement}}{{I-D.ietf-savnet-inter-domain-problem-statement}}.

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

- **SAV-specific Information:** The information that is specialized for SAV rule generation, includes the source prefixes and their legitimate incoming directions to enter a router or an AS, and is exchanged among routers or ASes.

- **SAV-related Information:** The information that can be used to generate SAV rules and includes SAV-specific Information and General SAV Information.

- **Source Entity (aka Source Router or Source AS):** The Entity (Router/AS) that propagates its SAV-specific information to Validation Entity (Router/AS) {{I-D.ietf-savnet-intra-domain-architecture}}{{I-D.ietf-savnet-inter-domain-architecture}}. Source Entity is the producer of SAV-specific information. 

- **Validation Entity (aka Validation Router or Validation AS):** The Entity (Router/AS) that receives SAV-specific information from Source Entity (Router/AS) {{I-D.ietf-savnet-intra-domain-architecture}}{{I-D.ietf-savnet-inter-domain-architecture}}. Validation Entity is the consumer of SAV-specific information. 

# Security Considerations {#sec-security}

This document provides an overview of terms and abbreviations related to SAV and does not have security considerations.

# IANA Considerations {#sec-iana}

There is no IANA requirement.

--- back


