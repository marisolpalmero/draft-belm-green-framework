---
title: "Framework for Energy Efficiency Management"
abbrev: "Framework for Energy Efficiency Management"
docname: draft-belmq-green-framework-latest
category: info
stand_alone: true

submissiontype: IETF
consensus: true

area: ""
workgroup: "Getting Ready for Energy-Efficient Networking"
keyword: Framework, Energy, Efficiency, Savings, Management

venue:
  group: "Getting Ready for Energy-Efficient Networking"
  type: ""
  mail: "green@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/green/"
  github: "marisolpalmero/draft-belm-green-framework"
  latest: "https://marisolpalmero.github.io/draft-belm-green-framework/draft-belmq-green-framework.html"

v: 3

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


--- abstract

Recognizing the urgent need for energy efficiency, this document emphasizes the establishment of a management framework within the GREEN Working Group to standardize processes, optimize energy usage, and ensure interoperability. This framework will leverage collected data from existing use cases to deliver actionable metrics for optimized energy management and informed decision-making. Furthermore, the document proposes a framework for collecting timestamped telemetry data across domains, using YANG, metadata, and Time Series Databases for transparent and dependable results.

--- middle

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

<< TO_DO: proposal to be extracted from philatelist, adding Jan Lindblad as a co-author >>

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
{:numbered="false"}

<< TODO acknowledge. >>
