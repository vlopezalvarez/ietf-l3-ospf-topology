---
coding: utf-8

title: A YANG Data Model for Open Source Path First (OSPF) Topology

abbrev: OSPF Topology YANG
docname: draft-ogondio-opsawg-ospf-topology-00
workgroup: OPSAWG Working Group
category: std
ipr: trust200902

stand_alone: yes
pi: [toc, sortrefs, symrefs, comments]

author:
  -
    name: Oscar González de Dios
    org: Telefonica
    email: oscar.gonzalezdedios@telefonica.com
  -
    name: Samier Barguil Giraldo
    org: Telefonica
    email: samier.barguilgiraldo.ext@telefonica.com

  -
    name: Victor Lopez
    org: Nokia
    email: victor.lopez@nokia.com

#contributor:
#  -


--- abstract

This document defines a YANG data model for representing an abstract view of the provider network topology that contains Open Source Path First (OSPF)  information. This document augments the 'ietf-network' data model by adding OSPF concepts. 

The YANG data model defined in this document conforms to the Network Management Datastore Architecture (NMDA).


--- middle

# Introduction

Topology collection is a critical use case for the network operators because the network topology is an abstract representation of the physical nodes, links and network interconnections. Network  planning processes requires that the network resources are placed to meet the traffic demands requirements not just in terms of bandwidth or delay, but also for failure scenarios. Network operators does the network planning process as an offline process, which obtains the information not directly from the network, but from inventory or template information. The main reason for this process was that there was a lack of a dynamic and programmatic interfaces that can allow the planning tools to obtain such information.

Thanks to the definition of the ietf-network model in {{!RFC8345}} this situation changed, because network operators can use an API with dynamic topological information. On top of the work in {{!RFC8345}}, {{!RFC8346}} and {{!RFC8944}} extends the generic network and network topology data models with topology attributes that are specific to Layer 3 and Layer 2. However, there is not any model that exposes Open Source Path First (OSPF) information. This information is required in the IP/MPLS planning process to properly assess the required network resources to meet the traffic demands in normal and failure scenarios. 

The main objective of this model is to represent most relevant OSPF topology attributes.

This document defines a YANG data model for representing, managing and controlling the OSPF topology. The data model augments ietf-network module {{!RFC8345}} by adding the OSPF information.

This document explains the scope and purpose of the OSPF topology model and how the topology and service models fit together.

The YANG data model defined in this document conforms to the Network Management Datastore Architecture {{!RFC8342}}.

## Terminology and Notations 

This document assumes that the reader is familiar with the contents of {{!RFC8345}}. The document uses terms from those documents.

The terminology for describing YANG data models is found in {{!RFC7950}}, {{!RFC8795}} and {{!RFC8346}}.

## Requirements Language

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in  {{!RFC2119}}, {{!RFC8174}} when, and only when, they appear in all capitals, as shown here.

## Tree Diagram

Authors include a simplified graphical representation of the data model is used in {{ietf-l3-ospf-topology-tree}} of this document.
The meaning of the symbols in these diagrams is defined in {{!RFC8340}}.

## Prefix in Data Node Names

  In this document, names of data nodes and other data model objects are prefixed using the standard prefix associated with the corresponding YANG imported modules, as shown in the following table.

| Prefix | Yang Module            | Reference    |
| ------ | ---------------------- | ------------ |
| ospfnt | ietf-l3-ospf-topology  | RFCXXX       |
| yang   | ietf-yang-types        | {{!RFC6991}} |
{: #tab-prefixes title="Prefixes and corresponding YANG modules"}

RFC Editor Note:
Please replace XXXX with the RFC number assigned to this document.
Please remove this note.

# YANG Data Model for OSPF Topology

The abstract (base) network data model is defined in the "ietf-network" module of {{!RFC8345}}. The OSPF-topology builds on the network data model defined in the "ietf-network" module {{!RFC8345}}, augmenting the nodes with OSPF information, which anchor the links and are contained in nodes).

There is a set of parameters and augmentations that are included at the node level. Each parameter and description are detailed following:

* Network-types: Its presence identifies the OSPF topology type. Thus, the network type MUST be ospf-topology.
+ OSPF timer attributes: Identifies the node timer attributes configured in the network element. They are wait timer, rapid delay, slow delay and the timer type (linear or exponential back-off).
- OSPF status: contains the neighbours information.

There is a second set of parameters and augmentations are included at the link and termination point level. Each parameter is listed as follows:

* Interface-type
+ Area ID
+ Metric
- Passive mode

{: #ietf-l3-ospf-topology-tree}

# OSPF Topology Tree Diagram

{{fig-ietf-l3-ospf-topology-tree}} below shows the tree diagram of the YANG data model defined in module ietf-l3-ospf-topology.yang ({{ietf-l3-ospf-topology-yang}}). 

~~~~
{::include ../Yang/ietf-l3-ospf-topology.tree}
~~~~
{: #fig-ietf-l3-ospf-topology-tree title="OSPF Topology tree diagram"}

{: #ietf-l3-ospf-topology-yang}

# YANG Model for OSPF topology

Following the YANG model is presented.

~~~~
<CODE BEGINS> file "ietf-l3-ospf-topology@2022-03-07.yang"
{::include ../Yang/ietf-l3-ospf-topology.yang}<CODE ENDS>
~~~~
{: #fig-ietf-ospf-topolopy-yang title="OSPF Topology YANG module"}

# Security Considerations

  The YANG module specified in this document defines a schema for data that is designed to be accessed via network management protocols such as NETCONF {{!RFC6241}} or RESTCONF {{!RFC8040}}.  The lowest NETCONF layer is the secure transport layer, and the mandatory-to-implement secure transport is Secure Shell (SSH) {{!RFC6242}}. The lowest RESTCONF layer is HTTPS, and the mandatory-to-implement secure transport is TLS {{!RFC5246}}.

  The NETCONF access control model {{!RFC6536}} provides the means to restrict access for particular NETCONF or RESTCONF users to a    preconfigured subset of all available NETCONF or RESTCONF protocol operations and content.

  There are a number of data nodes defined in this YANG module that are writable/creatable/deletable (i.e., config true, which is the default).  These data nodes may be considered sensitive or vulnerable   in some network environments.  Write operations (e.g., edit-config) to these data nodes without proper protection can have a negative effect on network operations.

# IANA Considerations

  This document registers the following namespace URIs in the IETF XML registry {{!RFC3688}}:

    --------------------------------------------------------------------
    URI: urn:ietf:params:xml:ns:yang:ietf-l3-ospf-topology
    Registrant Contact: The IESG.
    XML: N/A, the requested URI is an XML namespace.
    --------------------------------------------------------------------

   This document registers the following YANG module in the YANG Module Names registry {{!RFC6020}}:

    --------------------------------------------------------------------
    name:         ietf-l3-ospf-topology
    namespace:    urn:ietf:params:xml:ns:yang:ietf-l3-ospf-topology
    maintained by IANA: N
    prefix:       ietf-l3-ospf-topology
    reference:    RFC XXXX
    --------------------------------------------------------------------

# Implementation Status

This section will be used to track the status of the implementations of the model. It is aimed at being removed if the document becomes RFC.

--- back

{: numbered="false"}

# Acknowledgments

The authors of this document would like to thank XXX.

This document was prepared using kramdown.
