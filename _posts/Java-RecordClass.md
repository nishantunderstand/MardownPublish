What are records?
Does records have hashcode or equals methods


https://medium.com/@toimrank/java-records-the-end-of-boilerplate-code-37cd8b439b0a
Cannocial Constructor


2. static variables declaration allowed inside record.
3. Instance variables declaration NOT allowed inside Student record.
4. 4. record NOT allowed to extend class.
5. 5. record allow us to implement interface.
6. 6. We can create methods inside record:
7. 7) Records are serializable.

https://dev.to/birajdar/records-in-java-2cd6


Do we really never need to implement equals() and hashCode() in Java 16 records?
NO 

However, we can explicitly override them when the default component-based equality doesn't satisfy our domain requirements.