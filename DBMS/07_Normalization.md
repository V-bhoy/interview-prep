## Normalization
- step towards DB optimization
- to avoid redundancy in the DB and not store redundant data.

## Functional Dependency
- relationship between PK attribute (usually, can be an entity also) of the realtion to the other attribute signifying that through PK , the other attribute can be found.
- X -> Y , X is Determinant, Y is Dependent.
### Types of FD
- Trivial FD
    - A -> B is a trivial FD if B is subset of A.
    - A -> A, B -> B are also trivial FD
- Non Trivial FD
    - A -> B is a non-trivial FD if B is not a subset of A.
    - A intersection B is null.
### Rules of FD
- Reflexive
    - A is a set of attributes and B is a subset of A then A->B holds, obvious.
- Augmentation
    - if B can be determined from A, then adding an attribute to this FD cannot change anything.
    - if A->B holds, AX -> BX also holds. X being set of attributes
- Transitivity
    - if A->B & B -> C then A -> C

### Problems with redundant data?
- insertion, updation, deletion anomalies (abnormalities) are introduced.
- Insertion Anomaly
    - When certain attribute cannot be inserted without the presence of other attribute/data.
    - Ex: A table has a record for storing student and his branch together, but you cannot insert a student without knowing branch or you cannot insert a branch without knowing student. Even if you add student with a null branch , you have to update later, which is increase in work and also duplicate date for branch gets stored.
- Deletion Anomaly
    - When certain deletion results in the unintended loss of some other important attribute/data.
    - In above example, if suppose we had onle one student in Mechanical branch and we delete that student, it also deletes the information about the university having mechanical branch.
- Updation Anomaly
    - When an update of single data value requires multiple rows of data to be updated.
    - Due to updation in many places, data inconsistency arises, if one forgets to update data at a specific place.
    - In the above example, if suppose the HOD of a branch changes, we need to update it in many records, which can also lead to data inconsistency if 1/2 records are not updated due to some reason.
- Due to these anomalies, DB size increases, DB performance becomes very slow
- To rectify these anomalies and its effect on DB, we use NORMALISATION.

## What do we do in normalisation?
- Decompose the table into multiple tables until SRP is achieved & link them using relationships.
- SRP -> Single Responsibility Principle -> the relation contributes to some single source of information.

## Types Of Normal Forms
### 1NF
- Every relation cell must have atomic value (attribute cannot be further divided, single value)
- Relation must not have multi-valued attributes
```
❌ Unnormalized Table (UNF):
StudentID Name  Subjects
1         Raj   Math, Science
2         Priya English, History
🔄 1NF Conversion:
StudentID  Name  Subject
1          Raj   Math
1          Raj   Science
2          Priya English
2          Priya History
✅ Each subject is now stored separately.
- Has repeated data
```
### 2NF
- Relation must be in 1NF
- No partial dependency (no non-key attribute should depend on part of a composite key).
- All non prime attributes must be fully dependent on PK
```
❌ 1NF Table (with Partial Dependency):
StudentID     CourseID    StudentName    CourseName
1              101         Raj            Math
2              102         Priya          Science
Here:
	•	Primary Key = (StudentID, CourseID)
	•	Problem: StudentName depends only on StudentID (not the whole composite key).
🔄 2NF Conversion:
Student Table
StudentID StudentName
1           Raj
2           Priya
Course Table
CourseID   CourseName
101         Math
102         Science
Enrollment Table
StudentID     CourseID
1              101
2               102
✅ No partial dependency.
```
### 3NF
- Relation must be in 2NF
- No transitivity dependency exists
   -  non prime attribute should not find a non prime attribute
   -  non-key column should not depend on another non-key column
```
❌ 2NF Table (with Transitive Dependency):
EmpID       EmpName      DeptID      DeptName
1            Ankit        D1          HR
2            Sneha        D2          IT
Primary Key = EmpID
DeptName depends on DeptID, which depends on EmpID → transitive dependency.
🔄 3NF Conversion:
Employee Table
EmpID          EmpName      DeptID
1              Ankit         D1
2              Sneha         D2
Department Table
DeptID       DeptName
D1            HR
D2            IT
✅ Removed transitive dependency.
```
### BCNF (Boyce-Codd Normal Form)
- Relation must be in 3NF
- For every functional dependency X → Y, X should be a super key.
   - we must not derive prime attribute from any prime or non-prime attribute
```
❌ 3NF Table (not in BCNF):
Course     Teacher
DBMS       John
OS         Mary
DBMS       Mary
Dependencies:
	•	A course can have multiple teachers
  •	But each teacher teaches only one course.
So: Teacher → Course (but Teacher is not a super key).
🔄 BCNF Conversion:
Teacher Table
Teacher   Course
John      DBMS
Mary      OS
✅ Now Teacher is a key in its own table.
```

## Advantages
- minimize data redundancy
- simplified database organisation
- data consistency is maintained


