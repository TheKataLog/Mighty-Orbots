# 1 Welcome to MightyOrbots
Repository MightyOrbots' solution to O'Reilly 2024 Architectural Kata Challenge.

# 2 Problem Space
## 2.1 Functional Requirements
From the problem statement, we extracted the following core requirements to guide our proposed architecture for the MonitorMe system.

**Data Ingestion:**
The system should be able to read data from eight different patient-monitoring equipment.
Vital sign data sources include heart rate, blood pressure, oxygen level, blood sugar, respiration rate, electrocardiogram (ECG), body temperature, and sleep status.

**Data Consolidation and Display:**
The system should consolidate the data from multiple sources into a single stream.
It should display data on a consolidated monitoring screen at nurses' stations.
Each patient's vital signs should be displayed, rotating between patients every 5 seconds.
The monitoring screen should have a maximum capacity of displaying vital signs for 20 patients per screen.

**Data Recording and Storage:**
MonitorMe must record and store the past 24 hours of all vital sign readings for each patient.
Medical professionals should be able to review patient history, filtering on time range and vital signs.

**Data Analysis and Alerting:**
The system should analyze each patient's vital signs for abnormalities or preset thresholds.
It should alert medical professionals if it detects issues such as a decrease in oxygen level or reaching preset thresholds like a temperature of 104 degrees F.
Alerts should be timely and configurable to meet the needs of medical staff.

**Fault Tolerance and High Availability:**
MonitorMe should remain operational even if individual vital sign devices or components fail.
It should implement high-availability mechanisms to minimize downtime and ensure continuous monitoring and alerting services.


## 2.2 Additional Requirements
**User Interface and Interaction:**
MonitorMe should provide an intuitive user interface for medical professionals to interact with the system.
It should allow medical staff to configure alert thresholds, view patient data, and access historical records.

**Security:**
Although not required in the first iteration, MonitorMe should meet high data security and privacy standards in the future.
It should ensure user authentication and authorization to maintain data security and privacy.
It should ensure secure data exchange between different components.

**Scalability:**
The system should be scalable to accommodate increasing number of patients and vital sign monitoring devices.
It should handle peak loads during periods of high patient activity without degradation in performance.

**Integration Capabilities:**
Support integration with existing healthcare systems and other medical software solutions.
Provide APIs or interfaces for interoperability with third-party systems and devices.


## 2.3 System Requirements
TBD

## 2.4 Users
TBD

## 2.5 Constraints and Assumptions
TBD

# 3 Solution Space
In this section, we describe user personas and usage pattern analysis, which we used to help us make specific architectural choices. Notably, these analyses guided the particular components in our architecture. Subsequently, we specify the priority of order of architectural characteristics, followed by the proposed architectural style.

## 3.1 User Persona Analysis
TBD

## 3.2 Usage Patterns
TBD

## 3.2 Architecture Charactersitics
**Availability**

Reason:
As MonitorMe's primary purpose is to monitor patients' vital signs in real time, any system downtime could delay the detection of critical health issues, leading to potential harm or even fatalities for patients. High availability is also needed to ensure that alerts for abnormal conditions are delivered promptly, enabling healthcare providers to respond quickly in emergencies.

Impact on Architecture:
Load balancing in the data ingestion module.
Extract-Load-Transform (ELT) architecture

**Data Integrity**

Reason:
Healthcare decisions and diagnoses rely on accurate and reliable patient data. Therefore, the MonitorMe system needs high data integrity, meaning the data across the system must be free from incorrect modification and loss.

Impact on Architecture:
Data schema and selection of database

**Data Consistency**

Reason:
The MonitorMe system must also ensure that the vital sign readings ingested, stored, and displayed reflect the current state of the patient's health. Such consistency is also necessary for informed decision-making and patient safety.

Impact on Architecture:
Data schema and selection of database

**Fault Tolerance**

Reason:
The MonitorMe system should maintain service while facing failures. The primary failure scenario is when one or more vital sign devices or software components fail. It is essential for the MonitorMe system to still function for monitoring, recording, analyzing, and alerting based on the available data.

Impact on Architecture:
Vital sign timeseries are stored and processed independently of other vital sign signals.
Ability to detect vital sign failures
Ability to alert a data/system administrator about the failures
Ability to seamlessly ingest data after a failed component recovers
Extract-Load-Transform (ELT) architecture

Note that for MonitorMe to tolerate failures of other hardware and software components, it must consider redundancy and replication at various levels of the system. This requirement could include deploying multiple instances of servers, databases, and other components across different physical locations or availability zones. However, these considerations have little impact on the software architecture. Therefore, we leave the discussion of such deployment considerations to a subsequent section of this document.

**Concurrency**

Reason:
TBD

Impact on Architecture:
TBD

**Performance**

Reason:
TBD

Impact on Architecture:
TBD

Given the Katas Challenge's objectives and our assumptions (discussed in previous sections), we decided to deprioritize interoperability, responsiveness, and scalability in the first iteration of MonitorMe.


## 3.3 Architecture Style
TBD
