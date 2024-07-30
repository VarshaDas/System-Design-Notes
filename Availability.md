## 1. Availability

**Definition:**  
Availability measures how often a system is operational and accessible. It is often expressed as a percentage of uptime over a specific period.

## Use Cases to Demonstrate Availability

### Use Case 1: E-commerce Website
An e-commerce website needs to be highly available to handle customer orders and browsing at all times. By implementing load balancers and failover systems, the website can ensure that it remains accessible even if one server fails.

### Use Case 2: Online Banking System
An online banking system must be available to allow customers to access their accounts and perform transactions. Using monitoring and alerts, along with redundancy in both hardware and data, the banking system can minimize downtime and ensure continuous availability.

**Key Concepts:**

- **Uptime:** The total time a system is functioning correctly.
- **Downtime:** The total time a system is not functioning.
- **Service Level Agreement (SLA):** Defines the expected availability and performance targets between service providers and customers.

**Common Metrics:**

- **99.9% Availability (Three Nines):** Allows for about 8.76 hours of downtime per year.
- **99.99% Availability (Four Nines):** Allows for about 52.6 minutes of downtime per year.
- **99.999% Availability (Five Nines):** Allows for about 5.26 minutes of downtime per year.

  ![Screenshot 2024-07-30 231101](https://github.com/user-attachments/assets/47bed28a-c76b-4abf-9379-2b7a61dc4e16)


**Strategies to Improve Availability:**

- **Failover Systems:** Automatically switch to a backup system in case of failure.
- **Load Balancing:** Distribute traffic across multiple servers to ensure no single server becomes a bottleneck.
- **Monitoring and Alerts:** Continuously monitor system performance and alert administrators to potential issues.


## Availability in Sequence vs Parallel

### Sequence
Overall availability decreases when two components are in sequence.

Availability (Total)=Availability (Foo)∗Availability (Bar)

For example, if both Foo and Bar each had 99.9% availability, their total availability in sequence would be 99.8%

### Parallel
Overall availability increases when two components are in parallel.

Availability (Total)=1−(1−Availability (Foo))∗(1−Availability (Bar))
For example, if both Foo and Bar each had 99.9% availability, their total availability in parallel would be 99.9999%.


## Availability vs Reliability
- **Availability:** Refers to the system being operational and accessible.
- **Reliability:** Refers to the system consistently performing its intended functions without failure.

If a system is reliable, it is available. However, if it is available, it is not necessarily reliable. High reliability contributes to high availability, but it is possible to achieve high availability even with an unreliable system.



