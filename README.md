# EX4 - PROGRAM THAT RECEIVES A MESSAGE FROM MESSAGE QUEUE AND DISPLAY THEM
## AIM :
To write a C program that receives a message from message queue and display them

## DESIGN STEPS :

### STEP 1 :

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### STEP 2 :

Write the C Program using Linux message queues API 

### STEP 3 :

Execute the C Program for the desired output. 

## PROGRAM :

### C program that receives a message from message queue and display them :
writer.c
``` 
#include <stdio.h> 
#include <sys/ipc.h> 
#include <sys/msg.h> 
struct mesg_buffer 
{ 
	long mesg_type; 
	char mesg_text[100]; 
} 
message; 
int main() 
{ 
    key_t key; 
	int msgid;
	key = ftok("progfile", 65); 
	msgid = msgget(key, 0666 | IPC_CREAT); 
	message.mesg_type = 1; 
	printf("Write Data : "); 
	gets(message.mesg_text); 
	msgsnd(msgid, &message, sizeof(message), 0); 
	printf("Data send is : %s \n", message.mesg_text); 
	return 0; 
} 
```
reader.c
```
#include <stdio.h>
#include <sys/ipc.h>
#include <sys/msg.h>
struct mesg_buffer
{
	long mesg_type;
	char mesg_text[100];
} 
message;
int main()
{
	key_t key;
	int msgid;
	key = ftok("progfile", 65);
	msgid = msgget(key, 0666 | IPC_CREAT);
	msgrcv(msgid, &message, sizeof(message), 1, 0);
	printf("Data Received is : %s \n",message.mesg_text);
	msgctl(msgid, IPC_RMID, NULL);
	return 0;
}
```




## OUTPUT :
![image](https://github.com/user-attachments/assets/abfb6839-518e-419e-8d8d-1a24748ab956)





## RESULT :
The C program that receives a message from message queue and display them are executed successfully.
