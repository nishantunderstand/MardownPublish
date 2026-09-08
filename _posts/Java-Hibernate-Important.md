

Hibernate Important Topic

Hibernate ORM
Reference
https://medium.com/@mohit.mourya.sbg/step-by-step-guide-to-basic-hibernate-implementation-d79730d5faa3
Evoulution
Subtopic 1
ORM
Connect Java Code to SQL Table
ORM is a bridge between Java objects and SQL tables; it can be database-first, Java-first, or both.
SessionFactory vs EntityManager Factory
SessionFactory Belongs to Hibernate
EntityManagerFactory Belongs to JPA
Both are Functionally Same, But Work Differently
SessionFactory Vs Session Vs Transaction
Subtopic 1
SessionFactory Contains
Stores information about your entities(your classes that map to database tables).
Knows how those entities connect to each other (relationships).
Knows how everything maps to the database(which class goes to which table, etc.).
Holds the configurationyou gave Hibernate (dialect, settings, etc.).
Provides the tools/services Hibernate needsto talk to the database.
Subtopic 6
ThreadSafe
What is SessionFactory? (Thread-safe, immutable factory for Sessions.)
Session
New Session
openSession()
Not ThreadSafe
Curren Session
getCurrentSession()
Not ThreadSafe
Why isn’t Session thread-safe? (Scoped per transaction.)
Transactional
A Transaction belongs to a Session.
You start one by calling session.beginTransaction().
A Session can have many transactions, one after another.
But it should have only one active (uncommitted) transaction at a time.
Thread Safe : No, Don't it lead to Inconssient State. Is transaction thread-safe because only one thread uses it?
It is not about “internally thread-safe”; it is designed for single-thread ownership. Since one thread uses it, synchronization usually isn't needed.
single-thread ownership model
Transaction Interview Trap
“Why @Transactional on private method fails?”
“Can one @Transactional span multiple microservices?”
Query
SQL
HQL
JPQL
CriteriaAPI
JPA DerviedQuery Current 2026*
For Custom We can use @Query
@nativeQuery
NamedQuery
DerivedQuery
NamedQuery Vs NativeQuery
Entity Mapping Annotation
@Entity
Make Class as persistence
Without this it cannot be managed
Why should we not make an entity class final? (8:15)
@Table
@Id
Without this JPA cannot tracking
Because JPA must uniquely identify each entity instance.
@GeneratedValue
IDENTITY
@GeneratedValue(strategy = GenerationType.IDENTITY)
SEQUENCE
AUTO
@GeneratedValue strategies? (AUTO, IDENTITY, SEQUENCE, TABLE — default: AUTO.)
@Column
@Column(name = "emp_name", nullable = false, length = 100) private String name;
name, nullable, unique, length
@Transient
If we don't want to save the field in database
Difference @Transient vs transient keyword?
Relationship
@OneToOne
@OneToOne @JoinColumn(name = "passport_id") private Passport passport;
@OneToMany
@OneToMany(mappedBy = "department") private List<Employee> employees;
@ManyToOne
@ManyToOne @JoinColumn(name = "department_id") private Department department;
@ManyToMany
@ManyToMany @JoinTable( name = "student_course", joinColumns = @JoinColumn(name="student_id"), inverseJoinColumns = @JoinColumn(name="course_id") ) private Set<Course> courses;
Most Common
@ManyToOne
Directional ❓❓
How Many Tables Created ?
Subtopic 1
How does JOIN FETCH solve it? (Fetches associations in a single query.)
Purpose of @Version annotation? (Enables optimistic locking for concurrency control.)
Lock
OptimisticLock
Pestimitic Lock
Cache
L1-Cache
Single Http Request Session
L2-Cache
Perisitance Used with Redis ❓❓
What to Cache
Whatn't to Cache
What is Level-1 Cache? (Session-level, managed by Hibernate.)
What is Level-2 Cache? (Shared across sessions — reduces DB calls.)
What shouldn’t be cached in Level-2 cache? (Frequently changing or sensitive data.)
Hibernate LifeCycle
Entity states in Hibernate? (Transient, Persistent, Detached.)|
N+1 Problem
What is the N+1 Select Problem? (Lazy loading triggers multiple DB calls.)
Department Employees (One department has many employees) List<Department> deps = departmentRepo.findAll(); for (Department d : deps) { System.out.println(d.getEmployees().size()); } 1 query -> select * from department; N queries -> select * from employee where dept_id = ?
How to Fix it ?
Fetch Join
Entity Graph
Batch Size
Fetching Strategies
Eager
Lazy
Better Performance
Smaller initial Queries
Avoid Unnecessary joins / data loading
Better for Large Collections
Why ??
Why is FetchType.LAZY default for @OneToMany? (Prevents unnecessary data fetching.)
Fetch Types in JPA? (LAZY for on-demand, EAGER for immediate fetching.)
save , persist , merge
StoredProcedure
DB Procedure Example
CREATE PROCEDURE get_employee_count() BEGIN SELECT COUNT(*) FROM employee; END;
Why we need it ?
Bullk Salary Updae
Montly Payroll Processing
Large Reporting Queries
Legacy System
Why Company Prefer it ?
Faster for heavy DB Logic
Less network round trip
Reusable by multiple apps
Procedure should already be created in database
Repository
public interface EmployeeRepository extends JpaRepository<Employee, Long> { @Procedure(procedureName = "get_employee_count") Integer getEmployeeCount(); }
CascadeType
What are Cascade Types in JPA? (Propagate operations like persist or delete.)
CascadeType.REMOVE vs OrphanRemoval? (REMOVE cascades deletes; OrphanRemoval removes detached children.)
What happens to child entities if the parent is deleted? (Depends on cascade configuration.)
Rollback Types
Isolation Level
What is dirty checking? (Detects and updates changed entities automatically.)
CRUD Matrix
C — Create
Create One
Create All / Bulk Create
Create If Not Exists (idempotent create / upsert style)
Clone / Copy Existing Record (common in business apps)
R — Read
Read One
Read All
Read By Id
Read By Criteria / Filter
Read Paginated
Read Sorted
Read Projection (partial columns / DTO)
Read Aggregate (count, sum, avg)
Search Full Text
U — Update
Update One
Update All / Bulk Update
Update Partially (PATCH)
Replace Entire Record (PUT)
Upsert (insert if missing else update)
Increment / Decrement Field
Soft Update / Status Change (activate, deactivate)
D — Delete
Delete One
Delete All
Delete Completely (Hard Delete)
Soft Delete (mark deleted)
Bulk Delete
Delete By Criteria
Archive Instead of Delete

