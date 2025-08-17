## What is a transaction?
- sequence of sql operations to perform a task as a single unit.
- All these statements in a transaction either gets completed successfully or
  at any point if there is a failure, all the changes are undone, everything gets rollbacked.

## ACID Properties
- To ensure DATA INTEGRITY, we require DB system to maintain the ACID properties in a transaction.
### Atomicity
- either all operations are reflected in the DB or none of them are reflected in case of failure.
- A transaction should be executed completely or not executed at all.
- If one step fails, the entire transaction rolls back.
```
✅ Example:
Transferring amount from one account to another
It included debit from one account and credit to another account
If the credit step fails, then the debit step is rolled back → No money disappears.
```
### Consistency
- Integrity constraints must be maintained before and after transaction
-  A transaction should bring the database from one valid state to another valid state
  (respecting all constraints, rules, triggers).
```
✅ Example:
	•	Suppose balance >= 0 is a constraint.
	•	If a transaction tries to withdraw more money than available:
      If the account only has 3000, you try to withdraw 5000
      this violates consistency → the transaction is aborted.
```
### Isolation
- No Interference
- Multiple transactions running at the same time should not interfere with each other.
- Database ensures transactions behave as if executed serially (one after another).
```
✅ Example:
	•	Transaction 1 (T1): Transfer ₹1000 from A → B
	•	Transaction 2 (T2): Transfer ₹500 from A → C
If T1 and T2 run at the same time, isolation ensures A’s balance is updated correctly without lost updates.
If no isolation, suppose it has amount 4000 -> the amount could be 3000 / 3500 resulting in data inconsistency
```
### Durability
- Permanent Changes
- Once a transaction is committed, the changes are permanent even if system crashes.
- There must be a transaction recovery system to ensure durability.
```
✅ Example:
	•	You book a train ticket → money deducted and seat reserved.
	•	Even if the server crashes right after commit, your booking will still be valid when system restarts.
```
## Transaction States
### Active State
- When a transaction is executing its operations (read/write), it is in the Active state.
- It can move to either Partially Committed or Failed.
### Partially Committed State
- After the last statement of a transaction is executed but before changes are permanently saved (commit).
- System performs validation checks (constraints, integrity rules).
- Changes are saved in buffer in main memory
### Committed State
- When all operations are successful and COMMIT is executed.
- Changes become permanent (Durability).
- Trasaction moves to new consistent state, rollback cannot be done.
### Failed State
- 	If some error occurs (system crash, constraint violation, deadlock), transaction goes to Failed state.
- 	From here, it must be rolled back.
### Aborted State
- After a failed transaction is rolled back, it goes into Aborted state.
- DBMS restores database to previous consistent state.
### Terminated State
- Final state → transaction is finished (either committed or aborted).
- 	No further operations are possible.
### Transaction State Diagram
```
        ┌───────────┐
        │   Active  │
        └─────┬─────┘
              │
              ▼
   ┌───────────────┐
   │ Partially      │
   │ Committed      │
   └─────┬─────┬───┘
         │     │
   commit│     │failure
         ▼     ▼
   ┌───────────┐   ┌───────────┐
   │ Committed │   │   Failed  │
   └───────────┘   └─────┬─────┘
                          │ rollback
                          ▼
                    ┌───────────┐
                    │  Aborted  │
                    └─────┬─────┘
                          │
                          ▼
                    ┌───────────┐
                    │Terminated │
                    └───────────┘
```
## How to implement Atomicity and Durability?
- Recovery Mechanism Component supports atomicity and durability
### Shadow Copy Scheme
- Based on making shadow copies of DB
- assuming only one transaction T is active at a time
- a pointer called db-pointer is maintained on the disk, which points to current copy of DB
- T wants to update the DB, first it creates complete copy of DB
- all further updates are done on the new copy leaving the original copy untouched.
- If at any point of T has to be aborted, system deletes the new copy and the old copy is not affected.
- if T is successfull
    - OS makes sure all the pages of the new copy of DB written on the disk.
    - DB system updates the db-pointer to point the new copy of DB
    - New copy is now the current copy of DB
    - The old copy is deleted
    - The T is said to have been committed at the point where the updated db-pointer is written to disk.
- Atomicity
   - if a failure occurs before db-pointer is updated, the old content of DB are not affected.
   - T abort can be done by just deleting the new copy of DB.
   - Hence, either all updates are reflected or none
- Durability
   - Suppose, system fails at any time
   - When system restarts, it will read db-pointer and see the original content of the DB (that is pointer is still pointing to original copy) and none of effects of T visible.
   - T is assumed to be successful only when the db-pointer is updated.
   - If system fails, after the db-pointer has been updated, before that new copy was already written on the disk, when the system restarts,
     it will read new DB copy
- implementation is dependent on write to db-pointer being atomic. Luckily the disk system
  ensures that write to DB is either done / not done. it does not fail the process in between.
- It is inefficient because an entire DB is copied for every transaction.
### Log Based Recovery
- Log of each record is maintained in some stable storage so that if any failure occurs,
  it is recovered from there
- Any operation performed on DB is recorded in the log.
- The process of logging should be done before the actual txn is applied on DB
- Deferred DB Modifications
  - defers the execution of all write operations until the final action of txn is executed.
  - when txn is completed, the log information is used to execute write operations.
  - if system crashes before txn is committed / aborted, the log information is ignored.
  - if txn is committed, the log information is used to execute operations on DB
  - if failure occurs while updating DB, redo is performed.
- Immediate DB Modifications
  - The write operation is immediately executed on DB after the log is written
  - DB modifications by active txn are called uncommitted txns
  - In the event of crash / txn failure, system uses old field values of the log records to restore modified values.
  - Update takes place only after log records in a stable storage
  - Failure Handling
      - if system crashes before txn is committed / aborted, the old value of the txn is used to undo he txn.
      - if txn is committed, failure occurs, the new value field is used to redo the txn
### Checkpoint Based Recovery
- A checkpoint is like a snapshot of the database state at a specific point in time.
- It flushes all dirty pages (updated data in buffer but not yet written to disk) to disk.
- It writes a checkpoint record into the log file.
- It helps reduce the amount of work needed during recovery after a failure.
- Without checkpoints, after a crash the system would need to redo all committed transactions and undo all uncommitted transactions from the start of the log file → very slow.
- With checkpoints, recovery only needs to look after the last checkpoint, which makes recovery much faster.
```
  <T1 start>
<T1 update A>
<CHECKPOINT, T1, T2>
<T2 start>
<T2 update B>
<T1 commit>
<T3 start>
<T3 update C>
-- System Crash here

Recovery:
	•	From checkpoint: <CHECKPOINT, T1, T2>
	•	T1 → committed before crash → Redo.
	•	T2 → active, not committed → Undo.
	•	T3 → active, not committed → Undo.

So after recovery:
	•	Changes of T1 are permanent.
	•	Changes of T2 and T3 are rolled back.

 🔹 Advantages of Checkpoint-Based Recovery

✅ Faster recovery (don’t scan entire log, only after last checkpoint).
✅ Reduces overhead during system crash.
✅ Helps maintain consistency (Atomicity + Durability).

```
