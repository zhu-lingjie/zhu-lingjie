




### Application Stack 
In Linux, there are two distinct spaces, the user space and the kernel space. When the user runs an application, it will issue a system call, `read, write, open etc`,  then the kernel will allocate physical resources to the application. Also the application will have dependencies to the library. As illustrated by the graph below. 

![alt text](https://mermaidjs.github.io/mermaid-live-editor/#/view/eyJjb2RlIjoiZ3JhcGggTFJcbkFbPGI-QXBwbGljYXRpb248L2I-XS0tPGI-RGVwZW5kZW5jeSA8YnI-PC9iPi0tLSBCKExpYnJhcnkpXG5BLS0-QyhTeXN0ZW0gQ2FsbClcbkMtLT5EKExpbnV4IEtlcm5lbCkgXG5ELS0-RShQaHlpY2FsIFJlc291Y2VzIDxicj4gKiBSQU0gPGJyPipDUFUpXG5FLS0-IEFcblxuICAgIHN0eWxlIEEgZmlsbDojZjlmLHN0cm9rZTojMzMzLHN0cm9rZS13aWR0aDo0cHhcbiAgICBzdHlsZSBDIGZpbGw6I2NjZixzdHJva2U6I2Y2NixzdHJva2UtXG4iLCJtZXJtYWlkIjp7InRoZW1lIjoiZGVmYXVsdCJ9fQ) 
To trouble shoot application issues, usually they fall into: 
* Library dependency issues
* Issue can be resolved from syscall
























