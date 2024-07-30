## Replication

**Definition:**  
Replication is the process of copying data or services from one location to another to ensure data availability, reliability, and performance. It is crucial for maintaining consistency and redundancy in distributed systems.

**Types of Replication:**

- **Data Replication:**
  - **Master-Slave Replication:** One primary database (master) handles all write operations and updates. The changes are then replicated to one or more secondary databases (slaves) that handle read operations. This approach helps in load balancing and improves read performance.
  - **Master-Master Replication:** Multiple databases act as masters, allowing both to handle read and write operations. Each master replicates changes to the others, providing high availability and fault tolerance. Conflicts must be managed carefully to ensure data consistency.
  - **Peer-to-Peer Replication:** All nodes in the system are equal peers, and each node can act as both a source and a destination for replication. This model supports high availability and fault tolerance by distributing data across multiple nodes.

- **File Replication:**
  - **Real-Time Replication:** Files are replicated in real-time, ensuring that any changes made to the primary file are immediately reflected in the replica. This method is often used in high-availability systems where up-to-date data is critical.
  - **Scheduled Replication:** Files are replicated at scheduled intervals. This approach is useful when real-time replication is not necessary, and it can help reduce network load by avoiding constant data transfer.

- **Service Replication:**
  - **Stateless Replication:** Services are replicated without maintaining any session or state information. Each service instance handles requests independently, which simplifies replication but may require additional mechanisms to manage session state.
  - **Stateful Replication:** Services maintain state information and replicate it across instances. This approach is more complex but can provide a seamless user experience by preserving session state.

**Benefits of Replication:**

- **High Availability:** Ensures that data or services remain accessible even if one node or location fails.
- **Load Balancing:** Distributes requests or data access across multiple nodes, improving performance and reducing bottlenecks.
