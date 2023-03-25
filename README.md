#Project 4
#Multi-threaded Key-Value Store using RPC with PAXOS

##Assignment Overview
The purpose and scope of this assignment was to replace our 2-phase commit protocol from Project 3 with the paxos algorithm. 
The 2-phase commit protocol is not fault tolerant. If the coordinator goes down, the entire architecture grinds to a halt. 
This is because the coordinator is responsible for starting votes. Switching to the paxos algorithm allows the voting architecture to continue functioning as long as more than half of the nodes are functioning. 
This is because the nodes can communicate with each other, rather than only through the coordinator. The coordinator is a single point of failure.
	Similar to in Project 3, the client and server communicate via Java RMI (Remote Method Invocation).  Different from Project 3 is that the servers communicate directly with each other (using RMI),
 instead of through a coordinator. The flow of this architecture starts when a client writes a PUT, GET, DELETE command. This command is transmitted over RMI to any one of the 3 servers, which starts the paxos run. 
The servers gather promise and accept votes by accessing their own acceptor, as well as other acceptors over RMI. Once consensus has been reached, this accepted command is passed to all servers, 
where each server executes the commands locally. By carefully using synchronized methods and concurrent hashmap, we are able to keep the maps consistent. 
##Technical impression
The general theme for Project 4 was the same as in Project 3: The client is an HR person at a large company, trying to keep track of employee’s salaries. Because project 3 used a 2-phase commit protocol, it was NOT fault tolerant. 
For this reason, the company has opted to switch from 2-phase commit protocol to using the paxos algorithm. In doing so, the maps will maintain their consistent nature whilst server failures occur. 
All servers will contain their own proposers, acceptors, learners, and all servers will contain the same employee-salary map. This project was significantly harder than project 3 because 
the requirements (paxos algorithm, simulated server crashes) for this project were very unique, and very difficult to implement. Because of their difficulty, I spent lots of time on Google looking for resources. 
Because of the uniqueness, I had difficulties finding useful resources, and found very little relevant code.
	Thankfully, we were given several weeks to start work on this project and also an extension . Because of all this extra time, I was able to start multiple implementations 
(which ultimately did not pan out), without worrying too much about missing the deadline. In addition, with the generous aid of the TA’s, the professor, and the students of Piazza, 
I was able to have a much better understanding of the project requirements which I had not had prior to (such as needing to reset the acceptors to allow new paxos runs). 

##How to Run

Here are the steps to run the program:

1. Run Server1 via "java -jar RunServer1.jar <IP_ADDRESS> <PORT_NUMBER>"

2. Run Server2 via "java -jar RunServer2.jar <IP_ADDRESS> <PORT_NUMBER>"

3. Run Server3 via "java -jar RunServer3.jar <IP_ADDRESS> <PORT_NUMBER>"

2. Run the Client via "java -jar RunClient.jar <IP_ADDRESS> <PORT_NUMBER>"

3. To execute a PUT command, type "PUT <String> <Integer>"

4. To execute a GET command, type "GET <String>"

5. To execute a DELETE command, type "DELETE <String>"

##Examples with description
Any of the servers can be choosen for the runs
This is just a quick explanation of how the code runs, I had a test run with:
PORT_NUMBER = 32000
IP_ADDRESS = 127.0.0.1
The IP_ADDRESS was my device's address as i ran this on my device. 
With all functionality being met. 
PUT Abdul 5000 - Adds abdul to the map
GET Abdul - returns the value of Abdul
DELETE Abdul - removes Abdul from the map
 
##Limitations/Notes
This project has some limitions and notes that would be listed below:
If the PORT_NUMBER isn't an Integer then there would be a flag.
If the PORT_NUMBER isn't an non-negative Integer less than 65536 then there would be a flag.
If the IP_ADDRESS isn't the traditional numbers seperated by "." then it would be flagged. 
You can only use GET, PUT, DELETE opperations followed by the required and valid inputs. 
As demonstrated above in examples with description.

##Citation
Used https://stackoverflow.com/questions/1459656/how-to-get-the-current-time-in-yyyy-mm-dd-hhmisec-millisecond-format-in-java
for a part of my code, which helped with getting date and time in the right format

used the Notes provided on canvas and class videos, used multiple of them.