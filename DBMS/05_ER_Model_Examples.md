## Steps to create ER Model
- identify entity sets
- identify its attributes and data types
- identify relationships
- identify relationship constraints --> mapping and participation

## Banking System
- Gather Requirements

### Requirements
- Banking System --> Branches
- Bank --> Customers
- Customers --> Accounts, take loan, has relationship manager
- Bank has employees
- Bank has accounts --> savings , current
- loan --> originated by branch
- loan --> payment schedules

### Entity Sets
- Branch
- Customer
- Employee
- Saving Account
- Current Account
- Loan
- Payment (Weak entity --> dependent on loan)
- Saving and Current A/C can be generalized to Account entity

## Attributes
- Branch
   - name
   - city
   - assets
   - liabilities
- Customer
   - id
   - name
   - address --> composite
   - contact --> multi valued
   - DOB
   - age --> derived
- Employee
   - id
   - name
   - address
   - contact
   - years of service --> derived
   - start date
- Generalized entity --> Account
   - Account no
   - balance
- Savings Account
   - interest rate
   - daily withdrawal limit
- Current Account
   - Per Transaction Charges
   - over draft amount
- Loan
   - loan no
   - amount
- Payment
   - payment no
   - date
   - amount
 
 ### Relationships and constraints
 - Customer borrows loan (M: N)
 - Loan originated by branch (N : 1)
 - Loan has scheduled payments (1: N)
 - Customer deposit account (M : N)
 - Customer banker employee (N : 1)
 - Manager manages employee (1 : N)

### ER diagram
``` 
Customer
  └── customer_id (PK)
  └── name
  └── address
  └── phone
  └── email
  └── dob
       │                                               current --> per txn charges, overdraft amount
       │1         n                                       |
       └───< Owns >─── Account------------------------< is a >---savings
                       └── account_number (PK)                      └── Interest rate
                       └── account_type                              └── daily withdrawal limit
                       └── balance
                       └── open_date
                       └── branch_id (FK)
                             │
                             │1        n
                             └──< Has >── Branch
                                           └── branch_id (PK)
                                           └── branch_name
                                           └── location
                                           └── manager_name

Customer
   │
   │1        n     1                    n
   └──< Takes >── Loan---------------->Payment (Weak entity)
                  └── loan_id (PK)
                  └── loan_type
                  └── amount
                  └── loan_date
                  └── status

Account
   │
   │1        n
   └──< Has >── Transaction
                └── transaction_id (PK)
                └── transaction_date
                └── amount
                └── type
```
## Facebook Database

### 🔷 1. User
	•	user_id (PK)
	•	name
	•	email
	•	password
	•	gender
	•	dob
	•	profile_pic
	•	created_at

⸻

### 🔷 2. Post
	•	post_id (PK)
	•	user_id (FK → User)
	•	content
	•	media_url (optional)
	•	created_at
	•	privacy_setting (public, friends, private)

⸻

### 🔷 3. Comment
	•	comment_id (PK)
	•	post_id (FK → Post)
	•	user_id (FK → User)
	•	content
	•	created_at

⸻

### 🔷 4. Like
	•	like_id (PK)
	•	user_id (FK → User)
	•	post_id (FK → Post, optional)
	•	comment_id (FK → Comment, optional)
	•	liked_at

⸻

### 🔷 5. Friendship
	•	friendship_id (PK)
	•	requester_id (FK → User)
	•	receiver_id (FK → User)
	•	status (pending, accepted, blocked)
	•	requested_at
	•	accepted_at

⸻

### 🔷 6. Message
	•	message_id (PK)
	•	sender_id (FK → User)
	•	receiver_id (FK → User)
	•	content
	•	sent_at
	•	read_status

⸻

### 🔷 7. Page
	•	page_id (PK)
	•	name
	•	category
	•	created_by (FK → User)
	•	created_at

⸻

### 🔷 8. Page_Like
	•	page_like_id (PK)
	•	user_id (FK → User)
	•	page_id (FK → Page)
	•	liked_at

⸻

### 🔁 Relationships Overview
	•	User ↔ Post → 1-to-many (a user creates many posts)
	•	User ↔ Comment → 1-to-many
	•	User ↔ Like → 1-to-many
	•	User ↔ User → many-to-many via Friendship
	•	User ↔ Message → 1-to-many (sender & receiver sides)
	•	User ↔ Page → many-to-many via Page_Like
	•	Page ↔ Post → (if supporting page posts)

⸻

### 🖼️ ER Diagram (Text Representation)
```
User
 └── user_id (PK)
 └── name, email, ...

    │ 1        n
    └──< creates >── Post
                     └── post_id (PK), user_id (FK)

    │ 1        n
    └──< comments >── Comment
                      └── comment_id (PK), user_id (FK), post_id (FK)

    │ 1        n
    └──< likes >── Like
                   └── like_id (PK), user_id (FK), post_id/comment_id (FK)

    │ m        m
    └──< friends with >── Friendship
                          └── requester_id (FK), receiver_id (FK), status

    │ 1        n
    └──< sends >── Message
                   └── sender_id (FK), receiver_id (FK)

    │ m        m
    └──< likes >── Page_Like
                   └── user_id (FK), page_id (FK)

    │ 1        n
    └──< owns >── Page
                  └── page_id (PK), created_by (FK)
```
