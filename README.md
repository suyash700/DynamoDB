# DynamoDB Operations using Boto3 (Practical)

## 📌 Objective

To implement basic and advanced operations on Amazon DynamoDB using Python (Boto3), including:

* Table creation with proper key design
* Global Secondary Index (GSI)
* Data insertion and querying
* Conditional updates
* Exception handling

---

## 🛠️ Technologies Used

* Python
* Boto3 (AWS SDK for Python)
* AWS CLI
* Amazon DynamoDB

---

## ⚙️ Prerequisites

1. Install Python (3.x)

2. Install required libraries:

   ```bash
   pip install boto3 awscli
   ```

3. Configure AWS CLI:

   ```bash
   aws configure
   ```

   Enter:

   * Access Key
   * Secret Key
   * Region: ap-south-1
   * Output format: json

---

## 🔐 IAM Permissions Setup

Initially, an error occurred:

```
AccessDeniedException: not authorized to perform dynamodb:CreateTable
```

<img width="1045" height="184" alt="Screenshot 2026-04-18 121907" src="https://github.com/user-attachments/assets/2268ecbb-33ee-46ff-9f7a-987cbda73f1b" />


### Fix:

* Go to AWS IAM Console
* Select user
* Add permission:

  * AmazonDynamoDBFullAccess
 
<img width="1045" height="184" alt="Screenshot 2026-04-18 121907" src="https://github.com/user-attachments/assets/2268ecbb-33ee-46ff-9f7a-987cbda73f1b" />


---

## 📁 Project Structure

```
dynamodb_practical/
│── config.py
│── create_table.py
│── insert_data.py
│── query_data.py
│── update_data.py
│── delete_data.py
```

---

## 🧱 Step 1: Create Table

* Table Name: Orders
* Partition Key: user_id
* Sort Key: order_date

  <img width="1021" height="804" alt="Screenshot 2026-04-18 122323" src="https://github.com/user-attachments/assets/68ed479b-a92d-46c2-ba78-172e5f74622d" />
<img width="1056" height="855" alt="Screenshot 2026-04-18 122240" src="https://github.com/user-attachments/assets/93a6ec9b-39d5-4c46-aadc-a0829b5dc110" />


### Key Design:

* Composite key ensures high cardinality
* Supports range queries

### GSI:

* Index Name: StatusIndex
* Partition Key: status
* Projection: ALL

  <img width="1917" height="910" alt="Screenshot 2026-04-18 121934" src="https://github.com/user-attachments/assets/b7c6cc10-c5e5-4ee7-9d71-5cd1ccb8dfea" />


---

## 📥 Step 2: Insert Data

Inserted sample orders with attributes:

* user_id
* order_date
* status
* amount

<img width="1021" height="804" alt="Screenshot 2026-04-18 122323" src="https://github.com/user-attachments/assets/263de493-c8fc-4487-a160-04946c467374" />


### Exception Handling:

* Handles throttling errors
* Retry logic implemented

  <img width="934" height="69" alt="Screenshot 2026-04-18 121942" src="https://github.com/user-attachments/assets/2e480494-c526-4938-ab25-00b7eb46bdb1" />


<img width="1919" height="908" alt="Screenshot 2026-04-18 122048" src="https://github.com/user-attachments/assets/9574b665-092a-4ad3-ac1e-5020d6dd95ce" />


---

## 🔍 Step 3: Query Data

### 1. Query using Primary Key:

* Fetch all orders for a specific user

### 2. Query using GSI:

* Fetch orders based on status (e.g., pending)

  <img width="1004" height="822" alt="Screenshot 2026-04-18 122335" src="https://github.com/user-attachments/assets/7690b34c-3f8b-45a2-b144-846cf82e404a" />


  <img width="942" height="198" alt="Screenshot 2026-04-18 122108" src="https://github.com/user-attachments/assets/e0f86294-9db2-4b05-af83-31b495e9e927" />

  <img width="1919" height="908" alt="Screenshot 2026-04-18 122048" src="https://github.com/user-attachments/assets/3f1fac81-a894-42cc-acaa-3f6554b8d462" />



---

## 🔁 Step 4: Conditional Update

* Updated order amount using:

  * ConditionExpression: attribute_exists(user_id)

### Purpose:

* Prevents updating non-existing items
* Avoids lost updates

<img width="1919" height="916" alt="Screenshot 2026-04-18 122458" src="https://github.com/user-attachments/assets/47cf9cfe-d6f1-492b-b982-bbc0fdd71811" />

### Verify:

<img width="927" height="60" alt="Screenshot 2026-04-18 122421" src="https://github.com/user-attachments/assets/e80ccf52-d125-4e4b-8bf9-a9bca8655cfe" />

---

## 🗑️ Step 5: Delete Data

* Deleted item using primary key (user_id + order_date)

  <img width="1024" height="513" alt="Screenshot 2026-04-18 122519" src="https://github.com/user-attachments/assets/2e1eb574-23e4-495e-90e7-8548501efeb1" />

<img width="656" height="48" alt="Screenshot 2026-04-18 122544" src="https://github.com/user-attachments/assets/51092620-0559-477f-904e-49b80daf519b" />

<img width="1919" height="903" alt="Screenshot 2026-04-18 122559" src="https://github.com/user-attachments/assets/69b3b8ce-359e-410b-8452-2034d10b1aa1" />



---

## ⚠️ Step 6: Exception Handling

Handled specific DynamoDB errors:

* ConditionalCheckFailedException
* ProvisionedThroughputExceededException

---

## ▶️ Execution Steps

Run files in this order:

```bash
python create_table.py
```

(wait for table creation)

```bash
python insert_data.py
python query_data.py
python update_data.py
python query_data.py
python delete_data.py
```

---

## 🏆 Key Features

### ✅ Key Design & Partitioning

* Used composite key (user_id + order_date)

### ✅ Global Secondary Index (GSI)

* Implemented StatusIndex for alternate queries

### ✅ Conditional Updates

* Used ConditionExpression

### ✅ Exception Handling

* Handled specific AWS errors with retry logic

---

## 🎯 Conclusion

This practical demonstrates efficient NoSQL database design using DynamoDB, including:

* Optimized querying using keys and indexes
* Data consistency using conditional updates
* Robust handling of runtime errors

---
## Author : Suyash Dahitule
---
