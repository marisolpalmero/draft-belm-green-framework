---
title: "Framework for Energy Efficiency Management"
abbrev: "Energy Efficiency Management Framework"
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

v: 3

author:

 -
    fullname: Benoit Claise
    organization: Everything OPS
    email: benoit@everything-ops.net
 -
    fullname: Luis M. Contreras
    organization: Telefonica
    email: luismiguel.contrerasmurillo@telefonica.com
 -
    fullname: Jan Lindblad
    organization: All For Eco
    email: jan.lindblad+ietf@for.eco
 -
    fullname: Marisol Palmero
    organization: Independent
    email: marisol.ietf@gmail.com
 -
    fullname: Emile Stephan
    organization: Orange
    email: emile.stephan@orange.com
 -
    fullname: Qin Wu
    organization: Huawei
    email: bill.wu@huawei.com

normative:

   RFC8348:
    title: A YANG Data Model for Hardware Management
    date: 2018-03
    target: https://www.rfc-editor.org/info/rfc8348

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

   PetraApi: I-D.draft-petra-green-api

   GreenUseCases: I-D.stephan-green-use-cases

   PowerAndEnergy: I-D.draft-bcmj-green-power-and-energy-yang

   GreenTerminology: I-D.draft-bclp-green-terminology

--- abstract

Recognizing the urgent need for energy efficiency, this document specifies a management framework focused on devices and device components within, or connected to, interconnected systems. The framework aims to enable energy usage optimization, based on the network condition while achieving the network's functional and performance requirements (e.g., improving overall network utilization) and also ensure interoperability across diverse systems. Leveraging data from existing use cases, it delivers actionable metrics to support effective energy management and informed decision-making. Furthermore, the framework proposes mechanisms for representing and organizing timestamped telemetry data using YANG models and metadata, enabling transparent and reliable monitoring. This structured approach facilitates improved energy efficiency through consistent energy management practices.

--- middle

# TO DO and Open Issues

* IEC60050 reference needs a new URL

The following topics remain open for further discussion points:

## Discovering Capabilities
- Enable automatic detection of power-saving features.
- Allow controllers to easily discover device-specific limits like transition time and duty cycle.

## Understanding Device Capabilities
- Explore if Energy Objects can support multiple sets of power states.
- Make power states clearly described and understandable.
- Represent these capabilities in a machine-readable format.

## Mapping Intents to Device Settings
- Develop ways to translate high-level energy goals (like "save energy at low utilization") into actual device configurations.
- Create a standard method to describe this mapping across systems.

## Handling Transitions and Ensuring Safety
- Consider how long it takes for an Energy Object to switch power states.
- Recommendation to standardize a data model for safe limits on frequency or speed of transitions to prevent device/component's damage.
- Model SLAs that include both performance (e.g., transition time) and device safety (e.g., cycle limitations).

## East-West Traffic/Energy Metrics
- Recommendation to standardize a data model for new equipment interconnected East-West with optimized energy consumption.


# Introduction

{{GreenUseCases}}, analyzing use cases such as the "Incremental Application of the GREEN Framework" and "Consideration of other domains for obtention of end-to-end metrics"  reveals the critical need for a structured approach to transitioning network devices' management towards energy-efficient operations, for:

* Standardization: Ensuring consistent practices across different devices and network segments to facilitate interoperability.
* Energy Efficiency Management: Providing guidelines to identify inefficiencies, look for the balance between energy usage and
  network/resource/component/capability utilization and implement improvements.
* Scalability: Offering solutions that accommodate growing network demands and complexity.
* Cost Reduction: Optimizing energy usage to lower operational costs and extend equipment lifecycles.
* Competitiveness: Enabling organizations to maintain a competitive infrastructure through enhanced sustainability.
* Environmental Impact: Supporting broader sustainability initiatives by reducing carbon footprints.
* Simplified Implementation: Streamlining the deployment of energy-efficient measures to minimize service disruptions.
* Security: Protecting sensitive operations related to power states and consumption.

This document specifies an Energy Management framework for devices
within, or connected to, communication networks, for the use cases
described in {{GreenUseCases}}.
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


Based on the framework, companion work has been initiated to develop a YANG data model for energy efficiency metrics {{PowerAndEnergy}}. This data model includes:

- power and energy reporting,
- reporting on the measurement accuracy,
- reporting on industry-standard certifications (such as 80 PLUS for Power Supply Units, Energy Star, etc) rather than requiring vendors to report granular precision metrics,
- translation of the framework's concepts into an implementable specification, relying on the hardware management models such as {{RFC8348}}.

## Terminology

The following terms are defined in {{GreenTerminology}} and EMAN Framework {{?RFC7326}}: Energy, Power, Energy Management, Energy Monitoring, Energy Control.

The following terms are defined in EMAN Framework {{?RFC7326}}, and cut/paste here for completeness:

Energy Management System (EnMS)
: An Energy Management System is a combination of hardware and
software used to administer a network, with the primary purpose of
Energy Management.

      NOTES:

      1. An Energy Management System according to ISO50001 (ISO-EnMS)
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
         preferred meaning of an EnMS.  The definition from ISO50001
         can be referred to as an ISO Energy Management System
         (ISO-EnMS).

Device
: A device is a piece of electrical or non-electrical equipment.
Reference: Adapted from [IEEE100].

Component
: A component is a part of electrical or non-electrical equipment
(device).
Reference: Adapted from [TMN].

Meter (Energy Meter)
: A meter is a device intended to measure electrical energy by
integrating power with respect to time.
Reference: Adapted from [IEC60050].

Power Inlet
: A power inlet (or simply "inlet") is an interface at which a
device or component receives energy from another device or
component.

Power Outlet
: A power outlet (or simply "outlet") is an interface at which a
device or component provides energy to another device or
component.

Power Interface
: A Power Interface is a power inlet, outlet, or both.

Power State
: A Power State is a condition or mode of a device (or component)
that broadly characterizes its capabilities, power, and
responsiveness to input.
Reference: Adapted from [IEEE1621].

Power State Set
: A Power State Set is a collection of Power States that comprises a
named or logical control grouping.

Energy Object
: An Energy Object represents a piece of equipment that is
part of, or attached to, a communications network that is monitored
or controlled or that aids in the management of another device for
Energy Management.


# Motivation

## Impact on Energy Metrics

The framework will significantly enhance the creation of energy metrics with actionable insights by:

* Standardizing Metrics: Establishing consistent measurement protocols for energy consumption and efficiency.
* Enhancing Data Collection: Facilitating comprehensive monitoring and data aggregation across devices.
* Supporting Real-time Monitoring: Enabling dynamic tracking and immediate optimization of energy usage.
* Integration Across Devices: Ensuring interoperability for network-wide data analysis.
* Providing Actionable Insights: Translating raw data into meaningful information for decision-making.
* East-West Traffic Impact: Addressing the growing energy footprint of East-West traffic in data centers and distributed systems by providing a framework for measuring and optimizing energy consumption in these environments.

## Current Device Readiness

While many modern networking devices have basic energy monitoring capabilities, these are often proprietary. The framework will define requirements to enhance these capabilities, enabling standardized metric production and meaningful data contributions for energy management goals.

## Why Now?

The decision to define the framework now, rather than later, is driven by:

* Immediate Benefits: Start realizing cost savings, reduced carbon footprints, and improved efficiencies.
* Rapid Technological Advancements: Aligning the framework with current technologies to prevent obsolescence.
* Increasing Energy Demands: Mitigating the impact of growing energy consumption on costs and sustainability.
* Regulatory Pressure: Preparing for compliance with existing and anticipated sustainability regulations.
* Competitive Advantage: Positioning organizations as leaders in sustainability and innovation.
* Foundational Work Ready: Building on the use cases and requirements established in Phase I.
* Proactive Risk Management: Minimizing risks associated with energy costs and environmental factors.
* Facilitate Future Innovations: Creating a platform for continuous improvements and adaptations.
* Stakeholder Engagement: Ensuring diverse perspectives are reflected for broader adoption.


In conclusion, establishing the framework for energy efficiency management now is strategic and timely, leveraging the current momentum of use cases and requirements to drive meaningful progress in energy efficiency management. Delaying its development could result in missed opportunities for immediate benefits, increased costs, and challenges in adapting to future technological and regulatory landscapes.

# Reference Model

   The framework introduces the concept of a Power Interface.
   A Power Interface is defined as an interconnection among devices
   where energy can be provided, received, or both. There are some
   similarities between Power Interfaces and network interfaces. A
   network interface can be set to different states, such
   as sending or receiving data on an attached line. Similarly, a Power
   Interface can be receiving or providing energy.

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
   different relationships among device(s)/component(s), as specified in
   this document, include power source, Metering, and Aggregation
   Relationships.


The GREEN Reference Model is represented in the {{fig-green-reference-model}}

~~~ aasvg
{::include art/green_ascii.txt}
~~~
{: #fig-green-reference-model title="GREEN Reference Model" }


The main elements in the framework are as follows:

* (a), (d) Discovery and Inventory

* (b), (c) GREEN Metrics

* (b), (e) Monitor energy efficiency

* (f) Control Energy Saving

* (g) API Service Interface: enables access for service consumption, enabling data retrieval , control, and integration through API, e.g., {{PetraApi}}.

The monitoring interface (e) obviously monitor more aspects than just power and energy,
(for example traffic monitoring) but this is not covered in the framework.

Note that the GREEN framework specificies logical blocks, however, the Energy Efficiency Management function might be implemented inside the device, based in {{RFC8348}}, in the controller, or a combination of both.

Even the current reference model implicitly assume a hierarchical network structure, this assumption acknowledges that modern networks have flatter and anticipate more distributed topologies.

The referene model covers every network device and component that has a unique identifiable ID and can represent or influence power or energy consumption. If the component can be uniquely identified, it can be modeled.

In scope:

- Devices
- Chassis,
- Line cards, modules, ports
- Power supply units (PSUs), fans, thermal units
- Accelerators, GPUs, NPUs
- Virtualized components where applicable
- Any element providing power, energy

A YANG extension will be introduced to capture Power Factor(PF), enabling controllers engines to accurately compute real power. PF is essential for accurately estimating real power consumption in AC-powered components, especially PSUs.

## Data Collection Architecture

### Telemetry Push Pattern

The framework recommends a push-based telemetry model for energy efficiency data collection, where network devices stream energy measurements to management systems rather than waiting for poll requests.

For energy monitoring specifically, push-based telemetry offers:

- Temporal accuracy: Energy consumption varies over time; push models capture variations that polling might miss.
- Reduced latency: Anomalies (power spikes, efficiency degradation) are detected immediately.
- Network and data collection efficiency: Eliminates repetitive poll/response cycles.
- Scalability: Controllers can subscribe once rather than poll continuously.

### Controller vs. Device Initiated

The framework supports both initiation models:

- Controller-Initiated:
  - Controller subscribes to energy objects from managed devices
  - Provides centralized control over monitoring scope and frequency
  - Enables dynamic adjustment of monitoring based on operational needs

- Device-Initiated**:
  - Devices can autonomously report critical energy events
  - Useful for threshold violations or hardware failures
  - Complements controller-initiated subscriptions

### UUID-Based Component Identification

Energy metrics are anchored to hardware components using UUIDs from the ietf-hardware model {{RFC8348}}:

- Each physical component (chassis, power supply, line card, etc.) has a stable UUID
- Energy metrics reference these UUIDs, enabling correlation with:
  - Component lifecycle (installation, replacement, decommissioning)
  - Inventory management systems
  - Warranty and support tracking
  - Asset management databases

Energy Efficiency workflows require stable, cross-system identity for devices and components. To support this, the GREEN Framework adopts a dual-UUID strategy, based on ietf-hardware YANG module defined in {{RFC8348}}:

1. Device-Provided UUID (read-only):

- Originates from hardware or firmware.
- Represents the authoritative physical identifier.
- Preference to follow IETF hardware YANG identity.

2. Controller-Generated UUID (read-write):

- Used by orchestrators, schedulers, etc.
- Supports correlation across datasets, lifecycle stages, or clouds.
- Maintains identifier mapping.

### Measurement Accuracy and Data Source Classification

## Measurement Accuracy Framework

Energy metrics vary significantly in quality and source: some represent direct sensor measurements with known precision, others are estimates from datasheets or even machine learning predictions. To enable informed decision-making and prevent misleading comparisons, the framework requires explicit accuracy classification for all power and energy data.

The framework defines three primary accuracy categories:

- Unknown Accuracy: Data accuracy cannot be determined, or measurements are unavailable due to sensor failures, powered-off components, or other operational constraints.
- Estimated Data: Values derived through indirect methods:
 - Static estimates: From manufacturer datasheets, nameplate ratings, or typical values (essential for UC 1, Incremental Deployment with legacy devices).
 - Historic estimates: Based on prior measurements of this specific system under similar operational conditions.
 - Learned estimates: Generated potentially by machine learning models predicting consumption from workload patterns (UC 15, AI Training Workloads)

- Measured Data: Direct, real-time sensor measurements with quantified precision:
- Bronze: ±30% accuracy for typical values.
- Silver: ±10% accuracy for typical values.
- Gold: ±5% accuracy for typical values.
- Red: ±2% accuracy for typical values.
- Ones: All non-zero digits are significant/valid.

### Framework Benefits

Explicit accuracy reporting enables:

- Weighted aggregation: High-precision measurements carry appropriate weight when calculating network-wide energy consumption
- Upgrade prioritization: Identify devices with low-accuracy reporting for sensor upgrades or replacement
- Compliance validation: Automated verification against regulatory thresholds requiring specific measurement precision
- Double-accounting prevention: Understand when PDU-level measurements (±2%) should override device estimates (±30%) to avoid counting the same energy twice (UC 13)
- Cross-domain correlation: Map accuracy expectations when integrating with external systems like 3GPP energy KPIs (UC 6)

The accuracy hierarchy uses YANG identities for extensibility, allowing vendors to define manufacturer-specific accuracy classes while maintaining interoperability through standardized base types. Implementation details are provided in the companion YANG data model {{PowerAndEnergy}}.

### Industry-standard certifications

<<TO_DO>>


## Typical Power Topologies

   The following reference model describes physical power topologies
   that exist in parallel with a communication topology. While many
   more topologies can be created with a combination of devices, the
   following are some basic ones that show how Energy Management
   topologies differ from Network Management topologies. Only the controller,
   devices and components, are depicted here, as the Network Domain Level
   remains identical.

 NOTE:

* "###" is used to denote a transfer of energy using Power Interface.

* "- >" is used to denote a transfer of information using Network Interface.

### Basic Power Supply

This covers the basic example of router connected to Power Outlet in the wall.

~~~ aasvg
{::include art/basic_power_ascii.txt}
~~~
{: #fig-basic_power title="Reference Model Example: Basic Power Supply" }

### Physical Meter with Legacy Device

This covers the basic example of device connected to wall Power Outlet,
with a Physical Meter placed in the wall Power Outlet, because the device
can not monitor its power, energy, demand.

~~~ aasvg
{::include art/physical_meter_ascii.txt}
~~~
{: #fig-physical_meter title="Reference Model Example: Physical Meter" }

When the EnMS discovers the physical meter, it must know for
which Energy Object(s) it measures power or energy. This is the
Metering Relatonship.

A Metering Relationship is a relationship where one Energy Object
measures power, energy, demand, or Power Attributes of one or more
other Energy Objects.  The Metering Relationship gives the view of
the Metering topology.  Physical meters can be placed anywhere in
a power distribution tree.  For example, utility meters monitor
and report accumulated power consumption of the entire building.
Logically, the Metering topology overlaps with the wiring
topology, as meters are connected to the wiring topology.  A
typical example is meters that clamp onto the existing wiring.

### Physical Meter with New Device

This covers the example of device connected to wall Power Outlet, with a Physical Meter placed in the wall Power Outlet, because the previous device was not able to monitor its power, energy, demand.

~~~ aasvg
{::include art/physical_meter_new_device_ascii.txt}
~~~
{: #fig-new_device title="Reference Model Example: Physical Meter with New Device" }


The most important issue in such a topology is to avoid the double counting in the Energy Management System (EnMS). The physical meter reports the Energy transmitted, while the connected Device/Component might also report its consumed Energy. Those two values are identical. Without the knowledge of this specific topology, that is the Metering Relationship between the two Energy Objects, the EnMS will double count the Energy consumed in the network.


### Power over Ethernet

This covers the example of a switch port (Power Outlet) the provides energy with Power over Ethernet (PoE) to a PoE end points (camera, access port, etc.).

~~~ aasvg
{::include art/power_over_ethernet_ascii.txt}
~~~
{: #fig-power_ethernet title="Reference Model Example: Power over Ethernet" }

Double counting is also an issue in such an example. The switch port, via its Power Outlet, reports the Energy transmitted, while the PoE End Point, via its Power Inlet, reports its Energy consumed.

A second issue in such an example is the control topology. The controller must have the knowledge that, if it shuts down the switch port, it will also switch off the connected PoE End Point, as a consequence. This is the Power Source Relationship.

A Power Source Relationship is a relationship where one Energy Object provides power to one or more Energy Objects. The Power Source Relationship gives a view of the physical wiring topology -- for example, a PoE End Point receiving power from a switch port over PoE or a data center server receiving power from two specific Power Interfaces from two different PDUs.

On top of that, there might be two control points for the PoE End Point. First the connected switch port but also the controller direct connection to the PoE End Point (f). Via this interface, the controller might for example put the PoE End Point to a lower Power State.



### Single Power Supply with Multiple Devices

This covers the example of a smart PDU that provides energy to a series
of routers in a rack.

~~~ aasvg
{::include art/multiple_devices_ascii.txt}
~~~
{: #fig-multiple_devices title="Reference Model Example: Single Power Supply with Multiple Devices" }

### Multiple Power Supplies with Single Device

~~~ aasvg
{::include art/multiple_power_ascii.txt}
~~~
{: #fig-multiple_power title="Reference Model Example: Multiple Power Supplies with Single Device" }


## Relationships

The framework for Energy Management need to describe a means to monitor and control devices and components, and it needs to describe the relationships among, and connections between, devices and components.

Two Energy Objects can establish an Energy Object Relationship to model the deployment topology with respect to Energy Management.

Relationships are modeled with a Relationship that contains the UUID of the other participant in the relationship, along with a Relationship type.

There are three types of relationships are Power Source, Metering, and Aggregations.

* A Power Source Relationship is a relationship where one Energy
  Object provides power to one or more Energy Objects.  The Power
  Source Relationship gives a view of the physical wiring topology
  -- for example, a data center server receiving power from two
  specific Power Interfaces from two different PDUs.

  Note: A Power Source Relationship may or may not change as the
  direction of power changes between two Energy Objects.  The
  relationship may remain to indicate that the change of power
  direction was unintended or an error condition.

* A Metering Relationship is a relationship where one Energy Object
  measures power, energy, demand, or Power Attributes of one or more
  other Energy Objects.  The Metering Relationship gives the view of
  the Metering topology.  Physical meters can be placed anywhere in
  a power distribution tree.  For example, utility meters monitor
  and report accumulated power consumption of the entire building.
  Logically, the Metering topology overlaps with the wiring
  topology, as meters are connected to the wiring topology.  A
  typical example is meters that clamp onto the existing wiring.

* An Aggregation Relationship is a relationship where one Energy
  Object aggregates Energy Management information of one or more
  other Energy Objects.  The Aggregation Relationship gives a model
  of devices that may aggregate (sum, average, etc.) values for
  other devices.  The Aggregation Relationship is slightly different
  compared to the other relationships, as this refers more to a
  management function.

In some situations, it is not possible to discover the Energy Object
Relationships, and an EnMS or administrator must manually set them.  Given
that relationships can be assigned manually, the following sections
describe guidelines for use.

## Power State Set

The Energy Object contains a Power State Set attribute that represents
a set of Power States a device or component supports.

A Power State describes a condition or mode of a device or component.
While Power States are typically used for control, they may be used
for monitoring only.

A device or component is expected to support at least one set of
Power States consisting of at least two states: an on state and an
off state.

The semantics of a Power State are specified by:

   * The functionality provided by an Energy Object in this state.

   * A limitation of the power that an Energy Object uses in this
      state.

   * A combination of the first two.

The semantics of a Power State should be clearly defined.  Limitation
(curtailment) of the power used by an Energy Object in a state may be
specified by:

   *  An absolute power value.

   *  A percentage value of power relative to the Energy Object's
      Nameplate Power.

   *  An indication of power relative to another Power State.  For
      example, specify that power in state A is less than in state B.

   *  For supporting Power State management, an Energy Object provides
      statistics on Power States, including the time an Energy Object
      spent in a certain Power State and the number of times an Energy
      Object entered a Power State.


There are many existing standards describing device and component
Power States. TO BE COMPLETED


## Power State Set Mapping and Intent

Defining and enforcing power states can be challenging, because each Energy Object's technical capabilities must be mapped to high-level operational intents for energy-efficient operation. The following examples illustrate how an Energy Object's power-saving capabilities can be aligned with typical intents:

- running at reduced capacity during predictable low-demand periods;

- lowering energy use while maintaining required performance levels;

- operating at a reduced service level when the site is on a backup power source during a grid outage.

By expressing such intents, a controller can decide which power state an Energy Object should enter at any given time and under what conditions.

### Capability Discovery

Identifying what power states an Energy Object supports is crucial for onboarding and integration, especially for legacy systems. Key discovery elements include:

- Whether the energy object supports multiple Power State Sets.
- Semantics and limitations of each state (e.g., absolute power, relative power).
- Transition characteristics, such as the time required to move between states.
- Energy Object-specific state transition constraints like frequency, which may limit energy-saving measures to avoid damaging the device/components.
- Impacts on measurement accuracy.



### Intent Mapping

The goal of intent mapping is to translate high-level energy-saving intents into specific device/component configurations. For example:

- An intent like "reduce power consumption at low utilization" might map to a predefined low-power state.
- Controllers may interpret intents variably, e.g., "run at half capacity but be ready to scale up if needed."

This is comparable to intent mapping in YANG-based systems, from high-level Customer-Facing Services (CFS) to Resource-Facing Services (RFS) and ultimately to device-specific configurations.

### SLA Considerations

Meanwhile saving energy, the device or component shouldn't drop below a certain performance threshold or allow a certain service reduction or degradation. Based on this, there are two kinds of service level expectations (SLAs) are associated with Power State behavior:

- Transition SLAs - e.g., the maximum time allowed to transition between states.
- Operational SLAs - e.g., device frequency or operational cycle limits that ensure long-term hardware health.

# Interfaces Usage Of the Framework

This section provides an overview of how the GREEN use cases described in
[draft-stephan-green-use-cases] interact with the framework interfaces defined in this document.

Each use case is characterized by the sequence of framework interfaces it invokes to achieve energy-efficiency objectives.

## Mapping of Use Cases to Framework Interfaces

The table {{green-uc-interfaces-usage}} maps each GREEN use case to the framework interfaces and summarizes how these are used:

- The first line shows the interface sequences.
- The second line briefly describes the functional purpose of that flow.

The notation `a->b->c` represents the flow between framework components as described in the {{fig-green-reference-model}}, where:

- (a) Discovery interface
- (b) Monitoring interface
- (c) Metrics interface

|---
|UC| Use Case | Interfaces Usages |
|-|:-|:-
|1| Incremental deployment | c; c->b; a->d->b->e |
| | of the GREEN Framework | 1,2: legacy; 3: GREEN WG support (i)|
|2| Selective Reduction of | e->b->c->f |
| | Energy Consumption | monitor->metrics->control|
|3| Reporting on Lifecycle | c->g |
| | Management | metrics / metadata->API or report |
|4| Real-time Energy Metering | b->c |
| | of Virtualised NFs | monitor->metrics |
|5| Indirect Energy Monitoring| b->f |
| | & Control | monitor aggregate->control |
|6| Consideration of Other | c->g->b |
| | Domains for End-to-End | metrics->cross-domain API-> |
| | Metrics | monitoring |
|7| Dynamic Adjustment via | b->f->c |
| | Traffic Levels | observe->control->update metrics |
|8| Video Streaming Use Case | b->c->f |
| | | monitor->metrics->control |
|9| WLAN Network Energy Saving | b->f |
| | | monitor->control |
|10| Fixed Network Energy | b->f |
| | Saving | monitor->control |
|11| Energy Efficiency Network | a->b->c->f->g |
| | Management | discover->monitor->metrics-> |
| | | control->API |
|12| ISAC-enabled Energy-Aware | --- |
| | Smart City Traffic Mgmt | not clearly specified |
|13| Double Accounting Open | c->g |
| | Issue | metrics / metadata->API |
|14| Energy Efficiency Under | b->f |
| | Power Shortage | monitor->control |
|15| Energy-Efficient Mgmt of | b->c->f |
| | AI Training Workloads | monitor->metrics->control |
|---
{: #green-uc-interfaces-usage title="Use Cases Interfaces Usage"}

Use Case 1 (Incremental Deployment) illustrates how the usage of the framework interfaces evolves during the lifecycle of a network or device group, starting with legacy reporting, which is represented by 1=(c) and 2=(c -> b) and progressively incorporating GREEN-specific components 3=(a -> d -> b -> e).


## Observations and Next Steps

The mapping in {{green-uc-interfaces-usage}} demonstrates that most GREEN use cases rely primarily on the monitoring and control interfaces, with discovery being used during initialization or lifecycle events.

To complement {{green-uc-interfaces-usage}}, {{FunctionalOverviewFramework}}  provides a higher-level functional view of the framework. It summarizes how the interface sequences relate to the three primary operational domains of **Discovery**, **Monitoring**, and **Control**, and shows how they align with use cases.

|---
| Functional Domain | Details | Related Use Cases | Maturity / Status |
|-|:-|:-|:-|-:
| **Discovery** | Identification and characterization of devices and capabilities. Telemetry/Data Inputs: Device inventory data, model, firmware version, supported energy features. Example Actions: Register device energy profile; advertise capability set. | UC 1, UC 11 | High |
| **Monitoring** | Collection of energy-related telemetry across network elements. Telemetry/Data Inputs: Power usage, utilization, operational state, temperature. Example Actions: Aggregate metrics; compute KPIs; detect anomalies. | UC 2-10, UC 15 | Medium |
| **Control** | Modification of configuration to improve energy efficiency. Telemetry/Data Inputs: Monitored metrics, thresholds, policies.  Example Actions: Adjust link speed; enable sleep; re-route load; trigger automation. | UC 2, UC 5-10, UC 14-15 | Low-Medium |
|---
{: #FunctionalOverviewFramework title="Functional Overview of Framework Domains (Merged Details)"}



This indicates that future work should prioritize:

- Enhancing the interoperability and extensibility of monitoring telemetry.
- Defining control policies and interfaces to support energy optimization actions.
- Clarifying cross-domain data exchange (interfaces *g*) for reporting and federation.

Combining both perspectives, the detailed interface mapping {{green-uc-interfaces-usage}} and the functional overview {{FunctionalOverviewFramework}}, offers a comprehensive picture of how the GREEN Framework can be applied to concrete network energy-efficiency scenarios.

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
provided energy; therefore, monitored data requires protection.
This protection includes authentication and authorization of entities
requesting access to monitored data as well as confidentiality
protection during transmission of monitored data.  Privacy of stored
data in an entity must be taken into account.  Monitored data may be
used as input to control, accounting, and other actions, so integrity
of transmitted information and authentication of the origin may be
needed.

# IANA Considerations

This document has no IANA actions.

# Acknowledgments

This framework takes into account concepts from the Energy MANagement
(EMAN) Framework {{?RFC7326}}, authors by John Parello, Benoit Claise,
Brad Schoening, and Juergen Quittek. The contribution of Luis M.
Contreras to this document has been supported by the Smart Networks
and Services Joint Undertaking (SNS JU) under the European Union's
Horizon Europe research and innovation projects 6Green (Grant
Agreement no. 101096925) and Exigence (Grant Agreement no. 101139120).


