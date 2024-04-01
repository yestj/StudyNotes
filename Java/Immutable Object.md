## **Immutable Object**

: An object whose state cannot be modified after it is created

\- Once an immutable object is instantiated, its internal state(the values of its fields) cannot be altered through any means.

#### **1\. Thread Safety**

\- In a multi-threaded envrionment, multiple threads can access an immutable object simultaneously without worrying about synchronization issues

#### **2\. Simplified Concurrency**

\- Since immutable objects cannot be modified, they can be safely shared among multiple threads without the ned for synchronization mechanisms such as locks or mutexes

\- The simplifies concurrent programming and reduces the risk of race conditions

#### **3\. Caching and Reuse**

\- Immutable objects can be cached and reused freely because their state cannot change

\- This can lead to performance improvements by avoiding unnecessary object creation

#### **4\. Easier Debugging**

\- Reduces the complexity of tracking down bugs related to unexpected state chanes

### **How to create an immutable object in Java  
**

#### **1\. Make Fields Private and Final**

\- Declare all fields of the class as private and final to ensure that they cannot be modified once initalized

#### **2\. Do Not Provide Setter Methods**

\- Omit setter methods for the fields to prevent external modification of the object's state

#### **3\. Declare the Class as Final**

\- Make the class final to prevent subclassing, which could potentially introduce mutable behavior

```
// Example of mutable behavior

public class Person {
    private final String name;
    
    public Person (String name) {
    	this.name = name;
    }
    
    public String getName(){
    	return name;
    }
}

public class NewPerson extends Person {
	
    private String newName;
    
    public NewPerson(String name) {
    	super(name);
        newName = name;
    }
    
    public void setName(String name) {
    	this.newName = name;
    }
    
    public String getName() {	//override
    	return this.newName;
    }
 }
 
Person person = new NewPerson("Erin");
System.out.println(person.getName());		// Erin
 
NewPerson newPerson = (NewPerson) person;
newPerson.setName("wow");

System.out.println(person.getName());		// wow
```

#### **4\. Ensure Mutable Objects are Immutable or Safely Copied**

\- If the class contains references to mutable objects (such as collections), ensure that these objects are either immutable themselves or are safely copied to prevent external modification

```
public final class Person {
    private final String name;
    private final List<Job> jobs;
    
    public Person(String name, List<Job> jobs) {
    	this.name = name;
        this.jobs = copy(jobs);
    }
    
    public String getName() {	return name;	}
    
    public List<Job> getJobs() {	return copy(jobs);	}
    
    public List<Job> copy(List<Job> jobs) {
    	List<Job> cps = new ArrayList<Job>();
        jobs.forEach(o -> cps.add(new Job(o.title, o.salary)));
        return cps;
    }
 }
```

#### **5\. Create Defensive Copies if Necessary**

\- If the class exposes references to mutable object via getter methods, consider returning defensive copies of these objects to prevent clients from modifying the internal state

```
public final Class Person {
    private final String name;
    private final Job job;	// Job is mutable
    
    public Person(String name, Job job) {
    	this.name = name;
        this.job = new Job(job.title, job.salary);
    }
    
    public String getName() {
    	return name;
    }
    
    public String getJob() {
    	return new Job(job.title, job.salary);
    }
}
```
