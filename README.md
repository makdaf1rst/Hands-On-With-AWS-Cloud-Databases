<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# 🗄️ AWS Cloud Databases Series

**Author:** Mack (Saqib Hossain)  
**Email:** saqibh49@gmail.com  
**Series:** Get Hands On with Cloud Databases - NextWork Cloud Engineering Roadmap

---

## 📋 Series Overview

A hands-on deep-dive into AWS database services through 4 projects. This series covers both relational and non-relational databases, from setting up an Aurora MySQL cluster and connecting it to a live web app, to loading and querying data in DynamoDB using the console and CLI. Each project builds upon the last, creating a well-rounded understanding of how to store, query, and serve data in the cloud.

**What I Built:**
- An Amazon Aurora MySQL cluster connected to an EC2 instance
- A full-stack web app powered by Apache, PHP, and Aurora
- DynamoDB tables with flexible schemas and varying attributes
- Advanced queries and cross-table transactions using AWS CLI

**Duration:** ~3.5 hours across 4 projects  
**Difficulty:** Beginner to Intermediate

---

## 🎯 Learning Objectives

By completing this series, I gained hands-on experience with:

✅ **Relational Databases** - Setting up Amazon Aurora MySQL clusters with read replicas  
✅ **Web App Integration** - Connecting EC2 instances to Aurora using PHP and MariaDB  
✅ **NoSQL Databases** - Creating and managing DynamoDB tables with flexible schemas  
✅ **Data Modeling** - Understanding items, attributes, partition keys, and sort keys  
✅ **AWS CLI Operations** - Creating tables, loading data, and running queries from the command line  
✅ **Transactions** - Performing atomic multi-table writes with DynamoDB transactions  
✅ **Capacity Management** - Configuring read/write capacity units and staying within Free Tier  
✅ **SSH & Terminal Access** - Connecting to EC2 instances and managing databases from a local terminal

---

## 📚 Project Index

### Phase 1: Relational Databases (Projects 1-2)

**1. [Aurora Database with EC2](https://github.com/makdaf1rst/aws-databases-aurora)**
- Created an Amazon Aurora MySQL cluster with database instances
- Launched an EC2 instance and configured key pairs for secure access
- Connected Aurora to EC2 for future data retrieval
- Learned why Aurora uses clusters for scalability and fault tolerance
- ⏱️ Duration: 30 minutes

**2. [Connect a Web App with Aurora](https://github.com/makdaf1rst/aws-databases-webapp)**
- Connected to an EC2 instance via SSH from a local terminal
- Installed Apache HTTP Server, PHP, and MariaDB for web app support
- Created a PHP config file with Aurora database endpoint details
- Built an HTML-powered web app that reads and writes to Aurora
- Validated the database connection by querying tables directly from the terminal
- ⏱️ Duration: 1.5 hours

---

### Phase 2: Non-Relational Databases (Projects 3-4)

**3. [Load Data into DynamoDB](https://github.com/makdaf1rst/aws-databases-dynamodb)**
- Created a DynamoDB table with partition keys and attributes
- Configured read/write capacity units and disabled auto-scaling to stay in Free Tier
- Used AWS CLI in CloudShell to batch-create tables and load data
- Explored how different items can have completely different attributes
- Compared DynamoDB's flexibility and speed advantages over relational databases
- ⏱️ Duration: 40 minutes

**4. [Query Data with DynamoDB](https://github.com/makdaf1rst/aws-databases-query)**
- Queried tables using partition keys and sort keys in the console
- Discovered DynamoDB's query limitations when filtering by non-key attributes
- Ran advanced queries in CloudShell with projection expressions and capacity tracking
- Performed cross-table transactions to atomically update multiple tables at once
- ⏱️ Duration: 1 hour

---

## 🛠️ Technologies & Services Used

**AWS Services:**
- Amazon Aurora (MySQL-compatible)
- Amazon DynamoDB
- Amazon EC2 (Elastic Compute Cloud)
- AWS CloudShell
- Amazon RDS (Relational Database Service)

**Tools & Concepts:**
- AWS CLI
- SSH & Key Pairs
- Apache HTTP Server
- PHP & MariaDB
- Partition Keys & Sort Keys
- Read/Write Capacity Units (RCUs/WCUs)
- DynamoDB Transactions
- JSON IAM Policies

**Command Line:**
- `aws dynamodb create-table` - Create DynamoDB tables
- `aws dynamodb batch-write-item` - Bulk load data into tables
- `aws dynamodb get-item` - Retrieve specific items
- `aws dynamodb transact-write-items` - Atomic multi-table operations
- `aws s3 ls` / `aws s3 cp` - S3 bucket operations
- `mysql` - Direct database connection and querying
- `ssh` - Secure remote access to EC2 instances

---

## 🎓 Key Takeaways

### Relational vs Non-Relational
- **Aurora** excels at structured, relationship-heavy data with consistent schemas
- **DynamoDB** shines with flexible schemas where each item can have different attributes
- **Aurora uses clusters** for handling large-scale workloads with automatic failover
- **DynamoDB uses capacity units** that can auto-scale to meet demand

### Database Integration
- **Web apps need middleware** - Apache, PHP, and MariaDB bridge the gap between EC2 and Aurora
- **Connection details matter** - Endpoint names, credentials, and config files tie everything together
- **Terminal access is essential** - Validating database connections directly from the command line

### DynamoDB Design Patterns
- **Partition keys** are required for every query — you can't filter by arbitrary attributes
- **Sort keys** add a second level of filtering within a partition
- **Transactions** enable atomic operations across multiple tables
- **Flexible schemas** mean items in the same table can have completely different attributes

### Cost Management
- **Free Tier awareness** - 25 GB storage, 25 RCUs, and 25 WCUs for DynamoDB
- **Disable auto-scaling** in development to avoid unexpected charges
- **Capacity planning** - 1 RCU = 2 reads/sec, 1 WCU = 1 write/sec

---

## 📊 Architecture Diagrams

### Aurora + EC2 Web App Architecture
```
┌─────────────────────────────────────────────────────────┐
│                         VPC                             │
│                                                         │
│  ┌──────────────────────┐  ┌──────────────────────────┐ │
│  │    Public Subnet     │  │     Private Subnet       │ │
│  │                      │  │                          │ │
│  │  ┌────────────────┐  │  │  ┌────────────────────┐  │ │
│  │  │ EC2 Instance   │  │  │  │  Aurora MySQL      │  │ │
│  │  │                │  │  │  │  Cluster           │  │ │
│  │  │ ┌────────────┐ │  │  │  │  ┌──────────────┐  │  │ │
│  │  │ │ Apache     │ │──│──│──│─►│ Writer       │  │  │ │
│  │  │ │ PHP        │ │  │  │  │  │ Instance     │  │  │ │
│  │  │ │ MariaDB    │ │  │  │  │  └──────────────┘  │  │ │
│  │  │ └────────────┘ │  │  │  │  ┌──────────────┐  │  │ │
│  │  └────────────────┘  │  │  │  │ Reader       │  │  │ │
│  │         ▲            │  │  │  │ Instance     │  │  │ │
│  └─────────│────────────┘  │  │  └──────────────┘  │  │ │
│            │               │  └────────────────────┘  │ │
│     ┌──────┴──────┐       │                          │ │
│     │  Internet   │       └──────────────────────────┘ │
│     │  Gateway    │                                     │
│     └─────────────┘                                     │
└─────────────────────────────────────────────────────────┘
         ▲
         │
    ┌────┴─────┐
    │  Users   │
    └──────────┘
```

### DynamoDB Data Model
```
┌─────────────────────────────────────────────────────┐
│                   DynamoDB Tables                    │
│                                                     │
│  ┌─────────────────────────────────────────────┐    │
│  │  ContentCatalog                             │    │
│  │  ┌─────────┬──────────┬─────────┬────────┐  │    │
│  │  │ Id (PK) │ Title    │ Price   │ ...    │  │    │
│  │  ├─────────┼──────────┼─────────┼────────┤  │    │
│  │  │ 202     │ "Lab"    │ $4.99   │ Type,  │  │    │
│  │  │         │          │         │ URL    │  │    │
│  │  ├─────────┼──────────┼─────────┼────────┤  │    │
│  │  │ 203     │ "Video"  │ $9.99   │ Video  │  │    │
│  │  │         │          │         │ Type   │  │    │
│  │  └─────────┴──────────┴─────────┴────────┘  │    │
│  │  * Each item can have different attributes   │    │
│  └─────────────────────────────────────────────┘    │
│                                                     │
│  ┌─────────────────────────────────────────────┐    │
│  │  Comment                                    │    │
│  │  ┌──────────┬─────────────┬──────────────┐  │    │
│  │  │ Id (PK)  │ DateTime    │ PostedBy     │  │    │
│  │  │          │ (Sort Key)  │              │  │    │
│  │  └──────────┴─────────────┴──────────────┘  │    │
│  └─────────────────────────────────────────────┘    │
│                                                     │
│  ┌─────────────────────────────────────────────┐    │
│  │  Forum                                      │    │
│  │  ┌──────────┬───────────┬────────────────┐  │    │
│  │  │ Name(PK) │ Comments  │ Threads        │  │    │
│  │  └──────────┴───────────┴────────────────┘  │    │
│  └─────────────────────────────────────────────┘    │
│                                                     │
│         ┌──────────────────────────┐                │
│         │  Transaction Example:    │                │
│         │  1. Add Comment item     │                │
│         │  2. Update Forum count   │                │
│         │  (Atomic operation)      │                │
│         └──────────────────────────┘                │
└─────────────────────────────────────────────────────┘
```

---

## 💡 Unexpected Learnings

Throughout this series, several insights stood out:

1. **Aurora is not just MySQL** - It's 3-5x faster and handles backups, failover, and scaling automatically through its cluster architecture

2. **Non-relational doesn't mean unstructured** - DynamoDB still requires careful planning around partition keys, sort keys, and access patterns

3. **You can't query DynamoDB by any attribute** - Unlike SQL databases, you must design your table around the queries you'll run

4. **Transactions work across tables** - DynamoDB can atomically update items in different tables in a single operation

5. **The terminal is essential** - Connecting to EC2 via SSH and querying databases from the command line is a core skill, not just a shortcut

6. **Capacity planning matters** - Understanding RCUs and WCUs is critical for both performance and cost control

7. **CLI is more versatile than expected** - Batch operations and transactions in the CLI opened my eyes to why data engineers prefer it

---

## 🚀 What's Next

This databases series is Phase 3 of the complete Cloud Engineering roadmap. Other phases include:

**Phase 1: Foundations** - S3 hosting and IAM security basics  
**Phase 2: Networking** - VPC architecture, peering, endpoints, and monitoring  
**Phase 4: Security** - KMS encryption, GuardDuty, Secrets Manager, CloudTrail monitoring  
**Phase 5: Containers & Compute** - Lambda, Kubernetes, Docker, three-tier apps  
**Phase 6: DevOps** - CI/CD pipelines, Terraform, CloudFormation, multi-cloud  
**Phase 7: AI on Cloud** - Amazon Lex chatbots, AI transcription, Lambda integration

---

## 📂 Documentation Links

**Individual Project Repositories:**
- [Project 1: Aurora Database with EC2](https://github.com/makdaf1rst/aws-databases-aurora)
- [Project 2: Connect a Web App with Aurora](https://github.com/makdaf1rst/aws-databases-webapp)
- [Project 3: Load Data into DynamoDB](https://github.com/makdaf1rst/aws-databases-dynamodb)
- [Project 4: Query Data with DynamoDB](https://github.com/makdaf1rst/aws-databases-query)

**External Resources:**
- [NextWork Cloud Engineering Roadmap](https://learn.nextwork.org/projects/aws-databases-aurora?explore=series:cloud%20engineer)
- [AWS Aurora Documentation](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/)
- [AWS DynamoDB Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/)

---

## 🤝 Connect With Me

💼 [LinkedIn](https://linkedin.com/in/saqibhos)  
📧 Email: saqibh49@gmail.com  
🐙 GitHub: [@makdaf1rst](https://github.com/makdaf1rst)  
📘 [Facebook](https://facebook.com/mackdaf1rst)  
📷 [Instagram](https://instagram.com/mackdaf1rst)  
🤖 [Reddit](https://reddit.com/user/Mak_Mark_One)

---

## 📝 License

This project documentation is for educational purposes as part of the NextWork Cloud Engineering curriculum.

---

## 🙏 Acknowledgments

Special thanks to **NextWork** for providing a structured, hands-on cloud engineering curriculum that emphasizes real-world scenarios and practical troubleshooting.

---

<div align="center">

**⭐ If you found this helpful, please star this repository!**

*Building secure, scalable cloud infrastructure one project at a time.*

</div>

---

<!-- Proudly created as part of NextWork's Cloud Engineering Roadmap -->
