IoC 
Inversion Of Control
Design Philophoshy
Where the Control of Object Creation and Dependency management is inverted.
i.e. Instead of creating object and managing its dependencies 
that responsibility is delegated to external entity i.e Spring Container.


Spring Container :
It is able to creating the object, 	
configuring them and 
wiring them togther by reading the metadata configuration metadata.

IoC Container Types	

1. Spring BeanFactory Container
    1. Lazy Object Creation
    2. Doesn’t Support i8n
    3. Doesn’t Support Annotation Scanning 
2. Spring Application Context
    1. SuperSet of BeanFactory
    2. Extends Spring Bean Factory 
    3. Eager Object Creation
    4. Support i8n
    5. Support Annotation Scanning