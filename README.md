**Network Design and Configuration Report: Albion University**


**1. Introduction**

This report outlines the network topology design and implementation for Albion University. The objective was to design a scalable, secure, and efficient network connecting the Main Campus and a Smaller Campus (situated 20 miles apart), along with connectivity to an external Cloud Email Server. The design supports four faculties distributed across distinct buildings, ensuring high availability and logical segmentation of traffic using VLANs and IP subnetting.



**2. Network Topology Design (Task 1)**

The network is divided into three primary zones: the Main Campus, the Smaller Campus, and the External Cloud.

**2.1 Main Campus**

The Main Campus is the core of the network, connecting three key buildings via a central distribution switch/router setup:

Building A (Administration & Business): This building houses the Management, HR, and Finance departments, as well as the Faculty of Business. To meet security requirements, VLANs were implemented here to isolate sensitive administrative traffic (HR/Finance) from the academic traffic (Business Faculty).

Building B (Engineering & Arts): This building hosts the Faculty of Engineering/Computing and the Faculty of Art/Design. A dedicated subnet was assigned here to separate their traffic from the administration.

Building C (IT & Student Labs): This building serves as the technical hub, hosting the University Web Server and the internal DHCP server (configured on the router). Student labs are also located here, isolated on their own network segment.

**2.2 Smaller Campus**

The Smaller Campus connects to the Main Campus via a serial WAN link (simulating the 20-mile distance). It hosts the Faculty of Health and Sciences. To adhere to the requirement of separation, Staff and Student Labs are on separate floors and separate IP subnets.

**2.3 External Connectivity**

A router representing the ISP/Cloud connects to the Main Campus. This provides access to the external Email Server.

**3. Configuration and Protocols (Task 2)**

The following protocols were configured to ensure connectivity and service delivery:

**Routing Protocols:**

RIPv2 (Routing Information Protocol version 2): Configured on all internal routers to handle dynamic routing between the Main and Smaller campuses. RIPv2 was selected for its simplicity and ability to handle the university's subnet masks (VLSM).

Static Routing: A static route was configured on the Gateway Router to direct traffic specifically to the external Cloud Server, simulating a connection to an ISP.

VLANs (Virtual Local Area Networks): Used specifically in Building A to separate Management, HR, and Finance. This reduces broadcast traffic and enhances security.

DHCP (Dynamic Host Configuration Protocol): The Main Campus Router was configured as a DHCP server to automatically assign dynamic IP addresses to staff devices in Building A, ensuring seamless connectivity for mobile administrative staff.

**4. Critical Evaluation and Appraisal (Task 3)**

**4.1 Performance**

The network performance is optimized by splitting the campus into separate broadcast domains. By placing the Faculty of Engineering on its own network, the heavy data traffic typical of computing labs does not congest the administrative networks in Building A. The WAN link is dedicated, ensuring consistent throughput between the two campuses.

**4.2 Scalability**

The hierarchical IP addressing scheme (Class C private addresses) allows for significant growth. Currently, only a portion of the available subnets is utilized. If a new faculty building is constructed, a new subnet can be allocated without reconfiguring the existing core network.

**4.3 Reliability**

Reliability is achieved through the use of dynamic routing (RIPv2). If the network topology changes, the routers will automatically update their routing tables without manual intervention.

**4.4 Security**

Security is a primary feature of this design:

Logical Segmentation: The most critical security measure is the use of VLANs in Building A. This ensures that a student or a guest in the Business Faculty cannot "sniff" or access packets meant for the HR or Finance departments.

Separate Subnets: Each faculty is on its own IP network, allowing for the future implementation of Access Control Lists (ACLs) to further restrict traffic if necessary.

Physical Security: Critical servers (Web and DHCP) are centralized in the IT Department (Building C), which would historically have restricted physical access.
