
> **“Is memory increasing because of legitimate workload, or because objects are being retained unnecessarily?”**



```

WHY did it grow?
       │
 ┌─────┼───────────┐
 ▼     ▼           ▼
Leak  Traffic   Configuration



             OOM
              │
              ▼
       WHAT FAILED?
              │
     ┌────────┼────────┐
     ▼        ▼        ▼
    Heap   Metaspace  Native
     │        │        │
     ▼        ▼        ▼
 Objects   Classes   Direct buffers
           loaded    Threads
                     Code cache








WHAT EVIDENCE?
       │
 ┌─────┼───────────────┐
 ▼     ▼               ▼
Logs  Metrics      Heap/Native dump




WHAT ACTION?
       │
 ┌─────┼───────────────┐
 ▼     ▼               ▼
Fix   Tune JVM     Reduce load



```



GC removes unreachable objects, not old objects.



1. Static collections
2. 2. Unbounded cache
3. 3. ThreadLocal
4. 4. List/Map accumulating data
5. 5. Listener/Callback registration
6. Missing Close Method / terminate / shutdown method 

Log 
Heap Dump
Analyse the Dump in Visual VM
Look which is not releasing the resource.


