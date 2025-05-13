---
title: "Framework for Energy Efficiency Management"
abbrev: "Framework for Energy Efficiency Management"
docname: draft-belmq-green-framework-latest
category: info
stand_alone: true

ipr: trust200902
area: "Operations and Management"
wg: "Getting Ready for Energy-Efficient Networking"
kw:
  - framework
  - energy
  - efficiency
  - savings
  - management
submissiontype: IETF
consensus: true

coding: utf-8
pi: [toc, sortrefs, symrefs]

venue:
  group: "Getting Ready for Energy-Efficient Networking"
  type: ""
  mail: "green@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/green/"
  github: "marisolpalmero/draft-belm-green-framework"
  latest: "https://marisolpalmero.github.io/draft-belm-green-framework/draft-belmq-green-framework.html"

author:

 -
    fullname: Benoit Claise
    organization: Huawei
    email: benoit.claise@huawei.com
 -
    fullname: Emile Stephan
    organization: Orange
    email: emile.stephan@orange.com
 -
    fullname: Luis M. Contreras
    organization: Telefonica
    email: luismiguel.contrerasmurillo@telefonica.com
 -
    fullname: Marisol Palmero
    organization: Cisco Systems, Inc.
    email: mpalmero@cisco.com
 -
    fullname: Qin Wu
    organization: Huawei
    email: bill.wu@huawei.com

normative:

informative:
   TMN:
    title: International Telecommunication Union, "TMN management functions"
    date: 2000-02
    target: ITU-T Recommendation M.3400


   IEEE100:
    target: http://ieeexplore.ieee.org/xpl/mostRecentIssue.jsp?punumber=4116785
    title: The Authoritative Dictionary of IEEE Standards Terms
    author:
    - org: IEEE
    date: 2000-12-11

   IEEE1621: 
    title: Standard for User Interface Elements in Power Control of Electronic
     Devices Employed in Office/Consumer Environments, IEEE 1621
    author:
    - org: IEEE
    date: 2004-12


   IEC60050:
    target: http://www.iec.ch/smartgrid/standards/
    title: Power Utility Automation
    author:
    - org: IEC
    date: 2000-12-11


--- abstract

Recognizing the urgent need for energy efficiency, this document specifies a management framework within the GREEN Working Group to standardize processes, optimize energy usage, and ensure interoperability. This framework leverages collected data from existing use cases to deliver actionable metrics for optimized energy management and informed decision-making. Furthermore, the document proposes a framework for collecting timestamped telemetry data across domains, using YANG, metadata, and Time Series Databases for transparent and dependable results.

--- middle

# TO DO

- What we miss is the 4 reference examples rfc7326 section 4 
- Improve the abstract more in line with RFC 7326
- Add a link to the use case 2.5 (PoE)
- IEC60050 reference needs a new URL
- Nits: should this have its own rectangle? "(3) Network Domain Level :"



# Introduction


In reference to https://datatracker.ietf.org/doc/draft-stephan-green-use-cases/, analyzing use cases such as the "Incremental Application of the GREEN Framework" and "Consideration of other domains for obtention of end-to-end metrics", it reveals the critical need for a structured approach to transitioning network devices towards energy-efficient operations. The framework is essential for:

- Standardization: Ensuring consistent practices across different devices and network segments to facilitate interoperability.
- Efficient Energy Management: Providing guidelines to identify inefficiencies and implement improvements.
- Scalability: Offering solutions that accommodate growing network demands and complexity.
- Cost Reduction: Optimizing energy usage to lower operational costs and extend equipment lifecycles.
- Competitiveness: Enabling organizations to maintain a competitive edge through enhanced sustainability.
- Environmental Impact: Supporting broader sustainability initiatives by reducing carbon footprints.
- Simplified Implementation: Streamlining the deployment of energy-efficient measures to minimize service disruptions.
- Security: Protecting sensitive operations related to power states and consumption.

   This document defines an Energy Management framework for devices
   within, or connected to, communication networks, for the use cases
   described in https://datatracker.ietf.org/doc/draft-stephan-green-use-cases/.
   The devices, or the components of these devices (such as line cards, fans, and
   disks), can then be monitored and controlled. Monitoring includes measuring
   power, energy, demand, and attributes of power.  Energy Control can
   be performed by setting a device's or component's state.  The devices
   monitored by this framework can be either of the following:

   - consumers of energy (such as routers and computer systems) and
      components of such devices (such as line cards, fans, and disks)

   - producers of energy (like an uninterruptible power supply or
      renewable energy system) and their associated components (such as
      battery cells, inverters, or photovoltaic panels)

## Terminology

The following terms are defined in {{!I-D.draft-bclp-green-terminology}} and EMAN Framework {{?RFC7326}}: Energy, Power, Energy Management, Energy Monitoring, Energy Control.

The following terms are defined in EMAN Framework {{?RFC7326}}, and cut/paste here for completeness:

Energy Management System (EnMS)
      An Energy Management System is a combination of hardware and
      software used to administer a network, with the primary purpose of
      Energy Management.

      NOTES:

      1. An Energy Management System according to [ISO50001] (ISO-EnMS)
         is a set of systems or procedures upon which organizations can
         develop and implement an energy policy, set targets and action
         plans, and take into account legal requirements related to
         energy use.  An ISO-EnMS allows organizations to improve energy
         performance and demonstrate conformity to requirements,
         standards, and/or legal requirements.

      2. Example ISO-EnMS: Company A defines a set of policies and
         procedures indicating that there should exist multiple
         computerized systems that will poll energy measurements from
         their meters and pricing / source data from their local
         utility.  Company A specifies that their CFO (Chief Financial
         Officer) should collect information and summarize it quarterly
         to be sent to an accounting firm to produce carbon accounting
         reporting as required by their local government.

      3. For the purposes of EMAN, the definition herein is the
         preferred meaning of an EnMS.  The definition from [ISO50001]
         can be referred to as an ISO Energy Management System
         (ISO-EnMS).

Device
      A device is a piece of electrical or non-electrical equipment.

      Reference: Adapted from [IEEE100].

Component
      A component is a part of electrical or non-electrical equipment
      (device).

      Reference: Adapted from [TMN].

Meter (Energy Meter)
      A meter is a device intended to measure electrical energy by
      integrating power with respect to time.

      Reference: Adapted from [IEC60050].

Power Inlet
      A power inlet (or simply "inlet") is an interface at which a
      device or component receives energy from another device or
      component.

Power Outlet
      A power outlet (or simply "outlet") is an interface at which a
      device or component provides energy to another device or
      component.

Power Interface
      A Power Interface is a power inlet, outlet, or both.


Power State
      A Power State is a condition or mode of a device (or component)
      that broadly characterizes its capabilities, power, and
      responsiveness to input.

      Reference: Adapted from [IEEE1621].

Power State Set
      A Power State Set is a collection of Power States that comprises a
      named or logical control grouping.

# Motivation

## Impact on Energy Metrics

The framework will significantly enhance the creation of energy metrics with actionable insights by:

- Standardizing Metrics: Establishing consistent measurement protocols for energy consumption and efficiency.
- Enhancing Data Collection: Facilitating comprehensive monitoring and data aggregation across devices.
- Supporting Real-time Monitoring: Enabling dynamic tracking and immediate optimization of energy usage.
- Integration Across Devices: Ensuring interoperability for network-wide data analysis.
- Providing Actionable Insights: Translating raw data into meaningful information for decision-making.

## Current Device Readiness

While many modern networking devices have basic energy monitoring capabilities, these are often proprietary. The framework will define requirements to enhance these capabilities, enabling standardized metric production and meaningful data contributions for energy management goals.

## Why Now?

The decision to define the framework now, rather than later, is driven by:

- Immediate Benefits: Start realizing cost savings, reduced carbon footprints, and improved efficiencies.
- Rapid Technological Advancements: Aligning the framework with current technologies to prevent obsolescence.
- Increasing Energy Demands: Mitigating the impact of growing energy consumption on costs and sustainability.
- Regulatory Pressure: Preparing for compliance with existing and anticipated sustainability regulations.
- Competitive Advantage: Positioning organizations as leaders in sustainability and innovation.
- Foundational Work Ready: Building on the use cases and requirements established in Phase I.
- Proactive Risk Management: Minimizing risks associated with energy costs and environmental factors.
- Facilitate Future Innovations: Creating a platform for continuous improvements and adaptations.
- Stakeholder Engagement: Ensuring diverse perspectives are reflected for broader adoption.


In conclusion, establishing the framework for energy efficiency management now is strategic and timely, leveraging the current momentum of use cases and requirements to drive meaningful progress in energy efficiency management. Delaying its development could result in missed opportunities for immediate benefits, increased costs, and challenges in adapting to future technological and regulatory landscapes.

# Architecture Overview

   The framework introduces the concept of a Power Interface that is
   analogous to a network interface.  A Power Interface is defined as an
   interconnection among devices where energy can be provided, received,
   or both.

   The most basic example of Energy Management is a single device
   reporting information about itself.  In many cases, however, energy
   is not measured by the device itself but is measured upstream in the
   power distribution tree.  For example, a Power Distribution Unit
   (PDU) may measure the energy it supplies to attached devices and
   report this to an Energy Management System.  Therefore, devices often
   have relationships to other devices or components in the power
   network.  An Energy Management System (EnMS) generally requires an
   understanding of the power topology (who provides power to whom), the
   Metering topology (who meters whom), and the potential Aggregation
   (who aggregates values of others).

   The relationships build on the Power Interface concept.  The
   different relationships among devices and components, as specified in
   this document, include power source, Metering, and Aggregation
   Relationships.

   The framework does not cover non-electrical equipment, nor does it
   cover energy procurement and manufacturing.

 ~~~~


+--------------------------------------------------------------------+
|                                                                    |
|                  (3) Network Domain Level                          |
|                                                                    |
+--------------------------------------------------------------------+

(a)              (b)              (c)
Inventory        Monitor       +- DataSheets/DataBase and/or via API
Of identity      Energy        |  Metadata and other device/component
and Capability   Efficiency    |  /network related information:
     ^               ^         |
     |               |         |  .Power/Energy related metrics
     |               |         |  .information
     |               |         |  .origin of Energy Mix
     |               |         |  .carbon aware based on location
     |               |         |
     |               |         |
     |               |         |
     |               |         v
+--------------------------------------------------------------------+
|                   *                                                |
|     (2) controller   (collection, compute and aggregate?)          |
|                                                                    |
+--------------------------------------------------------------------+
             ^              ^                   ^ |
  (d)        |  (e)         |  (f)              | |(g)
  Inventory  |  Monitor     |  GREEN WG:        | | Control
  Capability |  Traffic     |  Monitor power    | | (Energy saving
             |  & power     |  Proportion,      | | Functionality
             |  consumption |  Energy efficiency| | Localized mgmt/
             |              |  ratio, etc)      | | network wide mgmt)
             |              |                   | |
             |              |                   | |
             |              |                   | v
+--------------------------------------------------------------------+
|                                            *                       |
|                       (1) Entities                                 |
|                                                                    |
| +---------+  +-----------+  +----------------+  +----------------+ |
| | (I)     |  | (II)      |  | (III)          |  | (IV)           | |
| |         |  |           |  | Legacy         |  | 'Attached'(PoE | |
| | Device  |  | Component |  | Device         |  | kind) Device   | |
| |         |  |           |  |                |  |                | |
| +---------+  +-----------+  +----------------+  +----------------+ |
+--------------------------------------------------------------------+

(*) Energy Efficiency Management Function is implemented inside the
device or in a controller

~~~~
{: #green-framework title="Framework discussed during the BoF"}

The main elements in the framework are as follows:

(a),(d) Discovery and Inventory

(b),(c) GREEN Metrics

(b),(f) Monitor energy efficiency

(e) Monitor power consumption and traffic (IPPM WG throughput, traffic load, etc)

(g) Control Energy Saving


## Typical Power Topologies




# Monitoring

to do

# Control

to do

# Conventions and Definitions

{::boilerplate bcp14-tagged}


# Security Considerations

Resiliency is an implicit use case of energy efficiency management
which comes with numerous security considerations :

Controlling Power State and power supply of entities are considered
highly sensitive actions, since they can significantly affect the
operation of directly and indirectly connected devices.  Therefore,
all control actions must be sufficiently protected through
authentication, authorization, and integrity protection mechanisms.

Entities that are not sufficiently secure to operate directly on the
public Internet do exist and can be a significant cause of risk, for
example, if the remote control functions can be exercised on those
devices from anywhere on the Internet.

The monitoring of energy-related quantities of an entity as addressed
can be used to derive more information than just the received and
provided energy; therefore, monitored data requires protection.  This
protection includes authentication and authorization of entities
requesting access to monitored data as well as confidentiality
protection during transmission of monitored data.  Privacy of stored
data in an entity must be taken into account.  Monitored data may be
used as input to control, accounting, and other actions, so integrity
of transmitted information and authentication of the origin may be
needed.


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments

This framework takes into account concepts from the Energy MANagement (EMAN) Framework {{?RFC7326}}, authors by John Parello, Benoit Claise, Brad Schoening, and Juergen Quittek.

{:numbered="false"}

