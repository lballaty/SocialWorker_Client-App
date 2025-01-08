### Database Related Design Document

---

#### **Objective**
This document outlines the database architecture and design for the Social Worker and Client Support App, ensuring scalability, security, and compliance with global regulations.

---

### **Database Design**

#### **1. Key Entities**
- **Users**:
  - Attributes: User ID, Name, Email, Role (Client, Social Worker, Admin), Language Preference, MFA Status.
- **Tasks**:
  - Attributes: Task ID, Title, Description, Type, Recurrence, Status (Pending, Completed, Overdue), Assigned User, Time of Day, Created At.
- **Messages**:
  - Attributes: Message ID, Sender ID, Receiver ID, Content, Timestamp.
- **Rewards**:
  - Attributes: Reward ID, User ID, Stars Earned, Badge Earned, Task ID, Timestamp.
- **System Logs**:
  - Attributes: Log ID, User ID, Event Type, Timestamp, Description.

#### **2. Relationships**
- One-to-Many: Social Workers to Clients.
- One-to-Many: Users to Tasks.
- One-to-Many: Tasks to Rewards.
- Many-to-Many: Users to Messages.

#### **3. Schema Overview**
- Tables:
  - `Users`
  - `Tasks`
  - `Messages`
  - `Rewards`
  - `SystemLogs`

---

### **Key Features**

#### **1. Data Integrity**
- Foreign key constraints to maintain relational consistency.
- Validation rules for critical fields (e.g., Email, Task Status).

#### **2. Anonymization and Compliance**
- Use of pseudonymization for anonymized data exports.
- GDPR-compliant data retention policies.

#### **3. Scalability**
- Partition tables by region for global data distribution.
- Use indexes for faster queries on frequently accessed fields (e.g., User ID, Task Status).

#### **4. Offline Support**
- Local caching of critical data (e.g., daily tasks) on client devices.
- Sync mechanisms for data consistency upon reconnection.

---

### **Workflows**

#### **1. Task Assignment Workflow**
1. Social worker creates a task and assigns it to a client.
2. Task is stored in the `Tasks` table with a reference to the assigned user.
3. Task appears in the client’s app upon next sync.

#### **2. Messaging Workflow**
1. User sends a message via the app.
2. Message is stored in the `Messages` table with references to sender and receiver IDs.
3. Receiver retrieves the message in real time or during the next sync.

#### **3. Reward Tracking Workflow**
1. Client completes a task and marks it as done.
2. Reward is generated and stored in the `Rewards` table.
3. Client’s progress tracker is updated with the new reward.

---

### **Next Steps**
- Validate schema design with database engineers.
- Implement indexing and partitioning strategies.
- Develop automated data sync and offline support mechanisms.

---

Prepared by: [Your Name or Team Name]  
Date: [Today's Date]

