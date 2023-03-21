# Academic-Projects
Following are some of the Academic projects completed as part of the <i>Computing Systems</i> specializing towards the **MS in Computer Science Program at Georgia Tech (2021 - 2022).**

<br><i>Note: As per the university and program policies, any project or course work is strictly prohibited from making public. Hence any code implementations for above assignments cannot be publicly posted. In case you wish to review, please reach out to me and I can provide the read only access to the my private repo for the above assignments.  </i>

## GETFILE 
**Course :** CS 6200 - Grad Intro to Operating Systems <br>
**Languages/Technologies :** C, Threads, Sockets, IPC Mechanisms <br>
An HTTP-like GETFILE protocol for file transfers between server & clients. Implemented multithreaded client and server with boss-worker pattern. 
Used mutexes and conditional variables for synchronized thread access to critical data sections.
Used server as a proxy where client requests the proxy and proxy further requests it from the cache instead of the webserver. 
The communication between proxy and cache uses IPC mechanisms. For implementing these IPC mechanisms, used the well-known **System V** standard.
<br><br> **Command channel**
- Through this the proxy sends the file request to the cache. This channel implemented using message queues. 
- Message queue is a queue in the kernel space to which messages can be placed by one process using msgsnd() and read by another process using msgrcv().

**Data channel**
- Through this the cache provides the actual content of the file to the proxy. The data channel uses the multiple shared memory IPC segments. 
- Once the cache receives this request from the proxy, the boss places the request in the cache queue and cache workers start processing them.
- Each cache thread maintains the request information such as the shared memory id, file name etc. Using the shared memory id, it retrieves the pointer pointing the data struct in the shared memory.
- Using the file name, the thread checks if the file is valid or not and and based on it performs the data transfer.


## DFS using gRPC
**Course :** CS 6200 - Grad Intro to Operating Systems <br>
**Languages/Technologies :** C++, gRPC, Remote Procedure calls, Protocol buffers <br>
A simple distributed file system using gRPC & protocol buffers where clients can perform fetch, store, list, delete & query the status of a file from the remote server.
RPC is a form of an inter process communication in which a process can request a service from another process which is on a remote system. That is, it is similar to invoking a procedure just placed remotely, to which certain details such as the function name, parameters required are sent via some message.
<br>

- gRPC is an open source remote procedure call framework created by Google
- RPC works with client-server models where there are separate stubs at each client and server end which carry out the remote procedure call.
- When the client invokes an rpc, it calls the client stub which marshals or packages the parameters and then this message is sent over to the server.
- The server OS sends it to the server-side stub which unmarshalls or unpacks the message parameter and implement the specified operation. Once complete, the result if any is returned in the same manner back to the client.
- The specifications of these procedures are described using IDL (Interface Definition Language) which can be thought of as a generic language which is independent of any systems or programming languages.
- Implemented simple RPCs and streaming RPCs.

## Spanning Tree
**Course :** CS 6250 - Computer Networks<br>
**Languages/Technologies :** Python, Learning Bridges<br>
A simplified distributed implementation of Spanning Tree protocol to prevent forwarding loops on layer 2 networks.
<br>

Brigdes operate on layer 2. It has multiple inputs/outputs through which it can receive and forward frames. Whenever a bridge receives a frame, its a learning opportunity to know which hosts are reachable through which port. This is how bridges learn and populate the forwarding table.
Unfortunately, if there is a loop in the network topology, then the packets will loop forever. To element these links that lead to loops, we run the Spanning tree algorithm. <br>

- The algorithm runs in rounds and at every round, each node sends configuration message to its neighbors with information such as node ID, ID of the perceived root and number of hops between the sending node and perceived root node.
- At first rond, each node thinks its the root. At every round, each node tracks and compares the messages received.
- Based on certain predefined criteria, most updated configuration is kept.
- The messages sent by nodes are maintained in a queue data structure. Once a node understands about the most optimial root node, it stops sending messaging.

## Distance Vector Routing
**Course :** CS 6250 - Computer Networks<br>
**Languages/Technologies :** Python, Bellman Ford Algorithm <br>

A simplified implementation of the Bellman-Ford algorithm to calculate routing distance between routers.
- Initialize all the neighbors of the source to the cost or distance between them. Rest are initialized to infinity cost.
- Each node maintains its own distance vector, with the cost to reach every other node in the network.
- From time to time, each node sends its own distance vector to its neighbor. Using that distance vector, each node updates its own vector.
- Each node update its vector using Dx(y) = min{cost(x, y) + Dv(y), Dx(y)} i.e. a node x computes the least cost to reach destination y by considering the options that it has to reach y through each of its neighbor v.


## Graph Search 
**Course :** CS 6601 - Artificial Intelligence<br>
**Languages/Technologies :** Python
<br>**Uninformed Search Algorithms**
<br>Blind search strategies where we do not have additional information about the states beyong the problem definition.
<br> (a) Breadth First Search (BFS) 
- Simplest Search starting from root. Each node at a certain depth in search tree is expanded before any othernodes at the next level. 
- It is achieved by using FIFO queue like data structure as the frontier where shallower nodes are at the front and deeper ones are added at the end.

<br> (b) Uniform Cost Search (UCS)
- Similar to BFS except, here we take into consideration costs between each node.
- We explore the node with the lowest path cost. For this we use a Priority Queue data struture.
- Unlike BFS, in UCS the goal test to see if reached target, is applied when the node is selected (popped from queue) for expansion as opposed to when its reached during exploration.

<br> (c) Depth First Search (DFS)
- It expands the deepest node in the frontier i.e. follows the path upto the leaf node.
- For this we use a LIFO Stack data structure.

<br>**Informed/ Heuristic Search Strategies**
<br>Here we have some more information about the problem or desire goal. The general approach is called best first serach where we select a node based on an evaluation function. So its like UCS with additional heuristic value.
<br> (a) Greedy Best First Search
- It tries to expand the node that is closer to the goal i.e. it evaluates nodes by using just the heuristic function such as straight line distance. 
- With this approach we never really expand a node that is far from the goal and we continually expand nodes that are closer to the final destination.

<br>(b) A* Search
- It combines the cost to reach the goal with an admissible heuristic. An admissible heuristic is the one that never overestimates the cost to reach the goal.
- Heuristics such straighline, Euclidean distance, Manhattan distance used for A* search.

<br>Implemented some of the above algorithms as Bidirectional/Tridirectional Searches. The idea is to start from 2 or more states. Motivation is to reduce the brnaching factor in the search tree. The search is stopped when the frontiers of these searches intersect.
Bidirectional & Tri-directional Breadth First Search (BFS), Uniform Cost Search (UCS) & A-Star algorithms for optimal path finding.


## Isolation Game
**Course :** CS 6601 - Artificial Intelligence<br>
**Languages/Technologies :** Python, Jupyter Notebooks, Numpy<br>
Created an AI using MiniMax and Alpha beta Pruning techniques that can play and win a game of **Skid Isolation game**. The created game is tested against several pre-baked AIs as well as peers’ AI systems. 
In the Skid Isolation, each player leaves behind traces when they move their queen. We say the queen "skids", and as a result the skid places a permanent block in the previously occupied block, the block "just before" the player's current position and the block "just after" the player's previous position. The opponent cannot move on or through squares blocked by this skid. 
Minimax & Alpha-beta Pruning implementations in an Isolation game. These algorithms use evaluation functions to minimize & maximize at each level to find the optimal move for the player.

<br>**Minimax Algorithm**
- It is a recursive algorithm used in adversial searches that helps in decision making in game theory. It helps in finding most optimal move for the player.
- Here we have two players MIN and MAX which are playing optimally. At each level, the opponent player's value is kept minimum and players score is maximized.
- The minimax algorithm is depth first search where all possible game moves are exlored and at the leaf, we have evaluation functions, whose scores are backtracked to the root.
- Here the evalution function returns the number of possible positions the queen can move.

<br>**Alpha Beta Pruning**
- This is an optimization technique for the minimax algorithm that helps in pruning or eliminating branches in the game tree exploration.
- Here additional alpha and beta values are maintained that can help in eliminating the nodes that do not affect the decision made at given level.

## Vacation Planner 
**Course :** CSE 6242 - Data Analytics and Visualizations<br>
**Languages/Technologies :** Python, FastAPI, Jupyter notebooks, Docker, Postgres SQL, Javascript, D3, AWS, Numpy, Data Analytics
- Developed a vacation planner which is an Airbnb optimizer that combines accommodations data and travel insights such as attractions and restaurants data together. 
- Studies have shown that vacation planning in today’s time can be a hectic task and time consuming task. In that, we have look at different websites, consider various factors such as destinations, hotels, fellow traveller’s preferences etc. Hence to simplifying this booking process and make it more personalized, brought together the Airbnb network data and Tripadvisor data together on a single platform.
- First the applications takes different user preferences such as type of stay, budget, restaurants and attractions that they are interested in as inputs. Then implement k-means clustering on Airbnbs, using geolocations. Clustering and filtering help in segmenting the airbnbs and eliminate the ones that don’t satisfy the user needs.
- One of the unique innovations of this app is weighted TSP calculation which helps inform user of the impact of choices they make eg. booking a cheaper stay farther away could cost more in terms of time required in commute. TSP is a known NP problem hence we utilize approximation solver’s like Dijkstra’s algorithm and external APIs like [MapBox](https://docs.mapbox.com/help/tutorials/optimization-api/). This route calculation helps in finding optimized routes from a certain Airbnb to the closest attractions and restaurants.
- The data required for this app is gathered from 3 sources - static Airbnb data.Sscraped and extracted the attractions/restaurants data from TripAdvisor using APIs. Obtained geodata for New York city from OpenstreetMaps. 

## Decision Trees & Random Forests 
**Course :** CS 6601 - Artificial Intelligence<br>
**Languages/Technologies :** Python, Jupyter Notebooks, Numpy, Data Analytics<br>
- Implemented Decision trees which is a supervised machine learning algorithms for a classification problem. Decision trees help in building a model from given set of data and labels, and then it can predict the target labels for a new data point. Used Gini Gain, Gini Impurity
metric to split the data into purer divisions. 
- In Decision trees, at every decision a greedy decision is made. Since this model is build using training data, it tends to over fit.
- To over come the over fitting, implemented Random Forests which is an ensemble learning technique that combines the outcome of various decision trees built by
sub-sampling.
- Created multiple decision trees by randomly sampling the data across data columns. The new data point is predicted across these multiple decision trees and majority is selected as the final prediction.

## Streaming Wars
**Course :** CS 6310 - Software Architecture and Design<br>
**Languages/Technologies :** Java, Postgres SQL, Docker, UML<br>
- Developed a system that allow users to track the different offerings from various streaming services and display usage measurements for the various services, in terms of number
of movies offered, dollars spent, etc. Implemented Java & Docker-based application simulating the interaction between various streaming services & studios. 
- Enchanced the application by providing Privacy of data by encrypting data to avoid exposing private information of the stakeholders. Used AES (Advanced Encryption Standard) which is a symmetric block cipher algorithm to encode sensitive data using 256 bit key size. 
- The transactional data such as financial and licensing details between studios and streaming services is encrypted before storing into the database.
- Developed design documents such as Class Diagrams, Sequence Diagrams, Deployment Diagrams of the system.

## RSA 
**Course :** CS 6035 - Information Security<br>
**Languages/Technologies :** Python <br>
- Implemeted hashing techniques & RSA algorithm using Fermat’s Factorization & Extended Euclidean Algorithm to find a private key from a vulnerable public key.
- RSA is public key scheme or asymmetric cryptography algorithm where there is no need for key exchange prioir to sending messages between parties. The algorithm is based on two keys - public key of the receiver is known and available. Anyone can encrpyt a message using this public key and send it. However only the receiver will be able to decrypt the message using the its private key.
- In RSA, we pick two prime values p and q such that N = pq is a very large number that is difficult to factorize. The security of RSA relies on the size of this number and difficulty of factorizing it.
- The public key provided in this task is vulnerable as it shares a common factor with other keys in the given list of public keys. This makes the key vulnerable as it is become easy to compute factorize and thereby decrpyt the message.

## Web Security 
**Course :** CS 6035 - Information Security<br>
**Languages/Technologies :** Javascript, PHP, SQL<br>
Performed target attacks such as Cross-Site Request Forgery (XSRF), Cross-Site Scripting (XSS) & SQL Injection to exploit vulnerabilities in an application.
- **Cross-Site Request Forgery (XSRF)** is a vulnerability where an attacker tricks user to perform certain actions. In this vulnerable application, I was able to manipulate the logged in user’s account and routing numbers using the html forms by performing the XSRF exploit. This exploit was successful because of the vulnerability of using hardcoded values to validate the POST request and insufficient mechanism to validate cookie session.
- **Cross-Site Scripting (XSS)** is an attack where an attacker can inject malicious script and browser executes it. In this vulnerable application, I could pass a hidden login variable to the main website in the form of POST request. Since the page directly loads and populates the POST[‘login’] value without any checking, I could insert the javascript snippet as value crafted in such a manner that it allowed creating <script> tag with my XSS exploit.
- **SQL Injection** is an attack in which SQL queries are injected in a manner that maliciously corrupts the database. Due to insufficient input validations, I could pass special filtering pattern in the sql queries that would then bypass the parameter checks.

## Branch Prediction, Cache Coherence & Performance of Out-of-Order Processors
**Course :** CS 6290 - High-Performance Computer Architecture<br>
Analyzed accuracy, speed-ups & overall efficiencies of different branch predictors (Taken/Not Taken/Hybrid/Tournament) & Cache Replacement policies (FIFO/LRU/Next LRU) using SMPCache simulator on multi-core
processors. Classified different types of read/write cache misses such as Capacity, Conflict, Compulsory and Coherence misses.

<br><i>Note: As per the university and program policies, any project or course work is strictly prohibited from making public. Hence any code implementations for above assignments cannot be publicly posted. In case you wish to review, please reach out to me and I can provide the read only access to the my private repo for the above assignments.  </i>


