+--+---------------------------+-------------------------------------+
|UC| Use Case                  | Interfaces Usages                   |
+--+---------------------------+-------------------------------------+
|1 | Incremental Application   | (c) ; (c)->(b) ; (a)->(d)->(b)->(e) |
|  | of the GREEN Framework    | 1,2 : legacy; 3 : GREEN WG support  |
|2 | Selective Reduction of    | (e) -> (b) -> (c) -> (f)            |
|  | Energy Consumption        | monitor -> metrics -> control       |
|3 | Reporting on Lifecycle    | (c) -> (g)                          |
|  | Management                | metrics / metadata -> API or report |
|4 | Real-time Energy Metering | (b) -> (c)                          |
|  | of Virtualised NFs        | monitor -> metrics                  |
|5 | Indirect Energy Monitoring| (b) -> (f)                          |
|  | & Control                 | monitor aggregate -> control        |
|6 | Consideration of Other    | (c) -> (g) -> (b)                   |
|  | Domains for End-to-End    | metrics -> cross-domain API ->      |
|  | Metrics                   | monitoring                          |
|7 | Dynamic Adjustment via    | (b) -> (f) -> (c)                   |
|  | Traffic Levels            | observe -> control -> update metrics|
|8 | Video Streaming Use Case  | (b) -> (c) -> (f)                   |
|  |                           | monitor -> metrics -> control       |
|9 | WLAN Network Energy Saving| (b) -> (f)                          |
|  |                           | monitor -> control                  |
|10| Fixed Network Energy      | (b) -> (f)                          |
|  | Saving                    | monitor -> control                  |
|11| Energy Efficiency Network | (a) -> (b) -> (c) -> (f) -> (g)     |
|  | Management                | discover -> monitor -> metrics ->   |
|  |                           | control -> API                      |
|12| ISAC-enabled Energy-Aware | ---                                 |
|  | Smart City Traffic Mgmt   | not clearly specified               |
|13| Double Accounting Open    | (c) -> (g)                          |
|  | Issue                     | metrics / metadata -> API           |
|14| Energy Efficiency Under   | (b) -> (f)                          |
|  | Power Shortage            | monitor -> control                  |
|15| Energy-Efficient Mgmt of  | (b) -> (c) -> (f)                   |
|  | AI Training Workloads     | monitor -> metrics -> control       |
+--+---------------------------+-------------------------------------+