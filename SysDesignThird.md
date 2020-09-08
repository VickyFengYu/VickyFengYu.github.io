# Optimistic and Pessimistic Locking

Traditional protection mechanisms, e.g. mistreatment synchronic keyword in java, is claimed to be hopeless technique of protection or multi-threading. It asks you to initial guarantee that no alternative thread can interfere in between sure operation (i.e. lock the object), so solely permit you access to any instance/method.

Though higher than approach is safe and it will work, however it place a big penalty on your application in terms of performance. 

There exist an additional approach that is more economical in performance, and it optimistic in nature. during this approach, you proceed with  update, being hopeful that you just will complete it while not interference. This approach depends on collision detection to work out if there has been interference from alternative parties throughout the update, during which case the operation fails and may be retried (or not).


## Concurrency

http://winterbe.com/posts/2015/04/30/java8-concurrency-tutorial-synchronized-locks-examples/


#### <i class="icon-file"></i>Pessimistic Locking

https://docs.gigaspaces.com/xap/12.1/dev-java/transaction-pessimistic-locking.html

See below example illustrating the usage of the exclusive lockup modality implementing pessimistic locking:

    @Transactional (propagation=Propagation.REQUIRES_NEW)  
	public void executeRescripts(Integer rescriptIDs[]) throws 	Exception  
	{  
    Rescript rescripts[] = new Order [rescriptIDs[].length];  
    for (int i=0;i<rescriptIDs.length;i++)  
    {  
        rescripts[i]= space.readById(Rescript.class, rescriptIDs[i],rescriptIDs[i],5000,ReadModifiers.EXCLUSIVE_READ_LOCK);  
        if (rescripts[i] != null)  
            rescripts[i].setStatus(DONE);  
    }  
    Object rets[] = space.updateMultiple(rescriptS, new long[rescriptIDs.size()], UpdateModifiers.UPDATE_ONLY);  
  
    for (int i=0;i<rets.length;i++)  
    {  
        if (rets[i] == null)  
        {  
            throw (new ReadTimeOutException("can't update object " + rescripts[i]));  
        }  
  
        if (rets[i] instanceof Exception)  
        {  
            if (rets[i] instanceof EntryNotInSpaceException)  
            {  
                throw (EntryNotInSpaceException)rets[i];  
            }  
            else if (rets[i] instanceof OperationTimeoutException )  
            {  
                throw (OperationTimeoutException)rets[i];  
            }  
            else  
	  {  
                throw (Exception)rets[i];  
	            }  
	        }  
	    }  
	}


#### <i class="icon-folder-open"></i>  Optimistic Locking

https://docs.gigaspaces.com/xap/12.1/dev-java/transaction-optimistic-locking.html

This example illustrates optimistic lockup usage while not employing a transactional update:

    @Transactional(propagation = Propagation.NEVER)  
	public void simpleOL() throws Exception {  
    Student employ = new Student("Last Name1", "First name1", new Integer(1));  
    studentspace.write(employ);  
  
    try {  
        //Read should not use a transaction!  
	  Student v1Employee = studentspace.readById(Student.class, new Integer(1), new Integer(1));  
        Student v2Employee = studentspace.readById(Student.class, new Integer(1), new Integer(1));  
        System.out.println("About to Write Version:" + v1Employee.getVersionID());  
        studentspace.write(v1Employee);  
        System.out.println("Student ID " + v1Employee.getStudentID() + " - Object version in Space:" +  
                v2Employee.getVersionID());  
        System.out.println("About to Write Version:" + v2Employee.getVersionID());  
        studentspace.write(v2Employee);  
    } catch (SpaceOptimisticLockingFailureException solfe) {  
        System.out.println("Got  " + solfe);  
        System.out.println("re-read Student Object again");  
        Student v3Employee = studentspace.readById(Student.class, new Integer(1), new Integer(1));  
        System.out.println("Perform update again. Client Object version:" + v3Employee.getVersionID());  
        LeaseContext<Student> leaseContext = studentspace.write(v3Employee);  
        if (leaseContext.getObject() != null)  
            System.out.println("Update Successful! Object version in Space:"  
	  + v3Employee.getVersionID());  
    }  
	}

#### <i class="icon-pencil"></i>  Compare and Swap Algorithm

https://howtodoinjava.com/core-java/multi-threading/compare-and-swap-cas-algorithm/

**Compare and Swap** is a good example of such optimistic method. 

This algorithmic rule compares the contents of a memory location to a given worth and, providing they're constant, modifies the contents of that memory location to a given new worth. this is often done as one atomic operation. The atomicity guarantees that the new worth is calculated supported up-to-date information; if the worth had been updated by another thread within the meanwhile, the write would fail. The results of the operation should indicate whether or not it performed the substitution; this will be done either with a straightforward mathematician response (this variant is usually known as compare-and-set), or by returning the worth browse from the memory location (not the worth written to it).

There are 3 parameters for a CAS operation:

1.  A memory location V where value has to be replaced
2.  Old value A which was read by thread last time
3.  New value B which should be written over V

Assume V could be a memory location wherever worth “10” is keep. There area unit multiple threads WHO wish to increment this worth and use the incremented worth for different operations, a really sensible situation.

**1) Thread 1 and 2 want to increment it, they both read the value and increment it to 11.**

_V = 10, A = 0, B = 0_

**2) Now thread 1 comes first and compare V with it’s last read value:**

_V = 10, A = 10, B = 11_

if     A = V
   V = B
 else
   operation failed
   return V

Clearly the value of V will be overwritten as 11, i.e. operation was successful.

**3) Thread 2 comes and try the same operation as thread 1**

_V = 11, A = 10, B = 11_

if     A = V
   V = B
 else
   operation failed
   return V

**4) In this case, V is not equal to A, so value is not replaced and current value of V i.e. 11 is returned. Now thread 2, again retry this operation with values:**

_V = 11, A = 11, B = 12_

And this time, condition is met and incremented value 12 is returned to thread 2.


#### <i class="icon-trash"></i> 


#### <i class="icon-hdd"></i>


----------

### Footnotes

[1] 
[2]
