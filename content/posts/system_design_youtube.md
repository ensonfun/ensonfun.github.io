Hi.
What do you think is a single most important component required for a successful system design interview?
What should we focus on the most while preparing for one?
I bet this is knowledge.
Knowledge of system design concepts and how to combine them together.
And let me prove you that by walking you through all the stages of a typical system design interview.
This is system design interview channel.
And today we discuss how to count things at a large scale.
So, the interviewer asks us to design a system that does counting.
The problem may be articulated clearly, for example we need to count views for videos on Youtube.
Or likes on Instagram or Facebook.
But more often than that, the problem will be stated in a vague or a more general manner.
For example, we may be asked to calculate not a single metric, like number of views, but a set of metrics.
For example we need to monitor performance of different applications.
Which means we need to count how many requests go through the service, how many errors service produce, average response time.
And of course nothing stops the interviewer from stating the problem in a very generic form, like analyze data in real-time.
What does data analysis mean?
Who sends us data?
Who uses results of this analysis?
What real-time really means?
These and many other questions need to be clarified.
And even if system design problem seems clear to you, let me give you two big reasons why you still need to ask your interviewer questions.
The first reason is really important for the interviewer.
The second reason is important for you.
The interviewer wants to see how you deal with ambiguity.
Whether you can identify key pieces of the system and define a scope of the problem.
And why it is so important for the interviewer - because she wants to understand how you will approach design problems in real life.
System design interview problems are usually open-ended.
It is impossible to solve such problems within 45 or 60 minutes interview.
We should be clear on what functional pieces of the problem we are going to focus till the rest of the interview.
And why requirements clarification is so important for us, interviewees?
Mainly because there may be many solutions to the problem asked.
And only when we fully understand what features of the system we need to design, we can come up with a proper set of technologies and building blocks.
For example, let's take a problem of counting Youtube video views.
If you ask this problem a software engineer with experience in SQL databases, he will explain you why MySQL database is a good fit.
Engineer with profound experience in NoSQL databases will explain how to count things at large scale using for example Apache Cassandra database.
We may use distributed cache to count stuff.
Or apply stream processing techniques.
Experts in cloud computing will solve this problem using public cloud services only.
Engineers focusing on batch processing will solve this problem using for example Hadoop MapReduce.
And views counting problem can indeed be solved using all these different approaches.
But these options are not equal.
Each has its own pros and cons.
We should pick those options that address requirements.
What we may want to ask about?
My recommendation is to focus on the following 4 big categories: Users, where we want to understand who and how will use the system.
Scale, where we want to understand how our system will handle a growing amount of data.
Performance, where we want to know how fast our system must be.
And cost, where we need to understand budget constraints.
Let's see what specific questions in each category we may ask.
Here and below we imply views counting system as an example.
Who will use the system?
Is this all Youtube viewers who will see the total views count for a video?
Or this is a per-hour statistics available to a video owner only?
Or may be this total count will be used by some machine learning models to generate recommendations.
How the system will be used?
The data may be used by marketing department only to generate some monthly reports.
In other words data is retrieved not often.
Or data is sent to recommendation service in real-time.
Meaning that data may be retrieved from the system with a very high pace.
Questions in this category help us understand what data we store in the system.
Questions in the Scale category should give us a clue how much data is coming to the system and how much data is retrieved from the system.
So, the questions we should ask: How many read queries per second the system needs to process.
How much data is queried per request.
How many video views per second are processed by the system.
Should we deal with sudden traffic spikes and how big they may be.
The interviewer will help us define these numbers.
Or we may assume some reasonable values.
Questions in the performance category should help us quickly evaluate different design options.
For example, if we can count views several hours later than these views actually happened, both batch data processing and stream processing design options can be considered.
But if time matters and we need to count views on the fly, or in other words in real-time, batch data processing is not an option.
It is just too slow.
Another good question to ask, is to clarify how fast data must be retrieved from the system.
And if interviewer tells us that response time must be as small as possible, it's a hint that we must count views when we write data and we should do minimal or no counting when we read data.
In other words data must already be aggregated.
And questions in the cost category should help us evaluate technology stack.
For example, if asked to minimize development cost, we should be leaning towards well-regarded open-source frameworks.
And if future maintenance cost is a primary concern, we should consider public cloud services for our design.
Here is a little secret you might already know.
During requirements clarification interviewer starts to understand your level of expertise in systems design.
As with coding interviews, if you do not ask questions, this is a warning sign for the interviewer.
And here is my advice: think along 4 categories mentioned here, think about data - what data, how it gets in and gets out of the system, and do not worry about time too much.
You better spend additional 5 minutes clarifying requirements and scope than find yourself solving a different or more complex problem than the interviewer actually asked.
The end goal of requirements clarification discussions is to get us closer to defining both functional and non-functional requirements.
When we say functional requirements, we mean system behavior, or more specifically APIs - a set of operations the system will support.
This is what our system will do.
And when we say non-functional requirements, we mean system qualities, such as fast, fault-tolerant, secure.
This is basically how a system is supposed to be.
Let's define functional requirements first.
And here is my practical advice.
After figuring out what the system should do, you write it down on the whiteboard.
In a few sentences.
For example, we write down that the system has to count video view events.
Count view events is the actual action the system performs and video becomes the input parameter.
And if we want the system to calculate not just views, but a broader set of events, let's say likes and shares, we may generalize our API a bit and introduce event type parameter.
This parameter indicates type of the event we process.
We can go one step further and make the system calculate not only count function, but other functions as well, like sum and average.
By supporting sum function we can calculate such metric as "total watch time" for a video.
While average function can help us calculate average view duration.
And we can even further generalize the API and say that the system will not just process events one by one, but a list of events as a single batch.
Where each event is an object that contains information about a video, type of the event, time when event happened and so forth.
Similar thought process can be applied for data retrieval API.
We first write down something like: the system has to return video views count for a time period.
Get views count becomes an action.
While video identifier and start and end time become input parameters.
If we want to retrieve count not only for video views, but for likes and dislikes for example, we can introduce event type parameter.
And if we want our API return not just count statistics, but also statistics for sum and average, we should specify function as a parameter and name our API in a more generic way, like getStats.
Following this simple technique will help you identify names of APIs, input parameters and, if needed, make several iterations to generalize APIs.
Now, let's talk about non-functional requirements.
Usually, the interviewer will not tell us specific non-functional requirements.
Most likely, she will challenge us with mentioning big scale and high performance, as it is hard to achieve both at the same time.
And we will need to find tradeoffs.
In one of the previous videos I recommended to focus on scalability, performance and availability as top priority requirements.
Let's use them here.
We need to design a system that should handle tens of thousands of requests per second.
We also want view count statistic to be returned in a matter of few tens of milliseconds.
And we want view count statistics to be shown to users all the time.
Even when there are network or hardware failures in the system.
Although these 3 will be our primary concern, let's also talk about two other interesting requirements.
Let's recall a CAP theorem and talk about consistency a bit.
And I would like us to touch a cost minimization topic.
And my advice is that you write down non-functional requirements on the whiteboard as well.
It will help you later while choosing among several design options.
We will talk more about this.
Now, we have come to the next stage of a system design interview: high-level architecture.
And we will start with something really simple.
We need a database to store data.
We will have a web service that processes incoming video view events and stores data in the database.
To retrieve view counts from the database, let's introduce another web service.
Nothing scary so far, right?
And it should not be.
At this point we do not yet have a clear vision of all pieces of the design.
So, we just throw some very high-level components to the whiteboard.
But what do we do next?
High chances the interviewer is an expert in the field and knows the question very well.
And she may start asking questions about any component we outlined in the high-level architecture.
But we may not feel comfortable discussing any component just yet.
Unless you are an expert in this field yourself, the whole picture may not yet be clear to you.
This is in our best interest as interviewees to drive the conversation and move forward one step at a time.
This is like assembling a puzzle.
The interviewer can assemble the puzzle starting from any color group.
But we need to start with something simple and construct the frame with the outside pieces first.
So, what is this frame of outside pieces of a system design puzzle?
It's data.
And more specifically we need to think what data we want to store and how.
Or using more professional terms we need to define a data model.
We have two options for what data we want to store.
We may store each individual video view event.
Or we may calculate views on the fly and store aggregated data.
When we store individual events we capture all attributes of the event: video identifier, timestamp, user related information such as country, device type, operating system and so on.
When we aggregate data we calculate a total count per some time interval, let's say one minute and we lose details of each individual event.
There are pros and cons of each option.
Individual events can be stored really fast.
We just get the event and push it to the database.
Later, when we retrieve data, we can slice and dice data however we want.
We can filter based on specific attributes, aggregate based on some rules.
And if there was a bug in some business report, we can recalculate numbers from scratch.
But there are drawbacks of this approach.
We cannot read data quickly.
We need to count each individual event when total count is requested.
This takes time.
Another big disadvantage of this approach - it may cost a lot of money to store all the raw events.
Youtube generates billions of view events per day.
Raw events storage must be huge.
On the other hand, reads become fast when we aggregate data.
We do not need to calculate each individual event, we just retrieve total count value.
Another nice property of the aggregated data, we can use it for decision making in real-time.
For example, we may send the total count value to a recommendation service or trending service, for popular videos to be promoted to trends.
Aggregated data approach has drawbacks as well.
First of all, we can only query data the way it was aggregated.
Ability to filter data or aggregate it differently is very limited.
This approach also requires us to implement data aggregation pipeline.
We need to somehow pre-aggregate data in memory before storing it in the database.
This is not an easy task and later you will see why.
Another big problem with this approach, it is hard or even impossible to fix errors.
Let's say we introduced a bug in the aggregation logic.
Then, how do we fix total counts after the bug was fixed?
So, which option should we chose?
Store raw events or aggregate data in real-time?
This is where we need interviewer to help us make a decision.
We should ask the interviewer about expected data delay.
Time between when event happened and when it was processed.
If it should be no more than several minutes - we must aggregate data on the fly.
If several hours is ok, then we can store raw events and process them in the background.
Former approach is also known as stream data processing, while latter is called batch data processing.
The interviewer will let us know what option she is interested the most.
But because I have no-one to ask...anybody...no...I will pick both options.
And by the way combining both approaches makes a lot of sense for many systems out there.
We will store raw events, and because there are so many of them, we will store events for several days or weeks only.
And then purge old data.
And we will also calculate and store numbers in real-time.
So that statistics is available for users right away.
By storing both raw events and aggregated data we get the best of both worlds: fast reads, ability to aggregate data differently and re-calculate statistics if there were bugs or failures on a real-time path.
But there is a price to pay for all this flexibility, the system becomes more complex and expensive.
Great topic to discuss with the interviewer.
Further in this video we will mainly focus on real-time aggregation option.
As I find it more educational from the system design perspective.
Now let's talk about where we store the data.
The interviewer wants to know specific database name and why we make this choice.
We should know (and do not worry if you do not know, you will know it in details in several minutes) that both SQL and NoSQL databases can scale and perform well.
So, we may want to evaluate both options.
And here is where we should recall non-functional requirements.
Remember that we wrote them down on the whiteboard before, right?
What are those?
Scalability, performance and availability.
So, we should evaluate databases against these requirements.
And let's add some more requirements along the way.
Feel free to use this list for other interview questions and system design in general.
Database solution we chose should scale well for both reads and writes.
It should be fast and guarantee high availability.
We should be able to achieve required level of data consistency.
We should understand how to recover data, achieve security, apply future data model changes.
We need to pick hardware and evaluate cost of the solution.
First, let's see how SQL databases handle these requirements.
Things are simple when we can store all our data on a single database machine.
But when a single machine is not enough, we need to introduce more machines and split data between them.
This procedure is called sharding or horizontal partitioning.
Each shard stores a subset of all the data.
And because we now have several machines, services that talk to the database need to know how many machines exist and which one to pick to store and retrieve data.
We discussed before that we have Processing service, that stores data in the database and Query service, that retrieves data from the database.
We could have made both these services to call every database machine directly.
A better option is to introduce a light proxy server that knows about all database machines and routes traffic to the correct shard.
Now, both Processing and Query services talk to this cluster proxy only.
They do not need to know about each and every database machine anymore.
But cluster proxy has to know.
Moreover, proxy needs to know when some shard dies or become unavailable due to network partition.
And if new shard has been added to the database cluster, proxy should become aware of it.
How do we achieve this?
We introduce a new component - Configuration service.
Configuration service maintains a health check connection to all shards.
So, it always knows what database machines are available.
So, cluster proxy calls a particular shard.
And instead of calling database instance directly, we can introduce one more proxy - shard proxy, that sits in front of a database.
Shard proxy will help us in many different ways: it can cache query results, monitor database instance health and publish metrics, terminate queries that take too long to return data and many more.
Great, this setup helps us address several requirements we mentioned before.
Like scalability and performance.
But availability is not yet addressed.
What if database shard died?
How to make sure data is not lost?
I believe you already know the answer to this question.
We need to replicate data.
Let's call each existing shard a master shard or a leader.
And for every master shard we introduce a copy of it, called read replica or a follower.
We call it read replica because writes still go through a master shard, but reads may go through both master shard and a replica.
We also put some replicas to a data center different from their master shard.
So that if the whole data center goes down, we still have a copy of data available.
So, when store data request comes, based on the information provided by Configuration service, cluster proxy sends data to a shard.
And data is either synchronously or asynchronously replicated to a corresponding read replica.
And when retrieve data request comes, cluster proxy may retrieve data either from a master shard or from a read replica.
Ideas we have just discussed is what Youtube is actually using.
They have built a database solution to scale and manage large clusters of MySQL instances.
It is called Vitess.
Great, we now know how to scale SQL databases.
But this solution does not seem simple, right.
We have all these proxies, configuration service, leader and replica instances.
May be we can simplify things a little bit.
Let's take a look at what NoSQL databases can offer us.
And more specifically, Apache Cassandra database.
In NoSQL world we also split data into chunks - shards, also known as nodes.
But instead of having leaders and followers we say that each shard is equal.
We no longer need configuration service to monitor health of each shard.
Instead, let's allow shards talk to each other and exchange information about their state.
To reduce network load, we do not need each shard to talk to every other shard.
Every second shard may exchange information with a few other shards, no more than 3.
Quickly enough state information about every node propagates throughout the cluster.
This procedure is called a gossip protocol.
Ok, each node in the cluster knows about other nodes.
And this is a big deal.
Remember that previously we used Cluster Proxy component to route requests to a particular shard.
As Cluster Proxy was the only one who knew about all shards.
But now every node knows about each other.
So, clients of our database no longer need to call a special component for routing requests.
Clients may call any node in the cluster and node itself will decide where to forward this request further.
Let's elaborate on this.
Processing service makes a call to store views count for some video B.
And let's say node 4 is selected to serve this request.
We can use a simple round robin algorithm to chose this initial node, or we may be smarter and chose a node that is "closest" to the client in terms of network distance.
Let's call this node 4 a coordinator node.
The coordinator node needs to decide which node stores data for the requested video.
We can use consistent hashing algorithm to pick the node.
As you may see node 1 should store the data for the video B.
Coordinator node will make a call to the node 1 and wait for the response.
Actually, nothing stops coordinator node to call multiple nodes to replicate data, for example 3 nodes if we want 3 copies of data.
Waiting for 3 responses from replicas may be too slow, so we may consider the write to be successful as soon as only 2 replication requests succeeded.
This approach is called quorum writes.
Similar to quorum writes, there is a quorum reads approach.
When Query service retrieves views count for video B, coordinator node 4 will initiate several read requests in parallel.
In theory, the coordinator node may get different responses from replica nodes.
Why?
Because some node could have been unavailable when write request happened.
That node has stale data right now, other 2 nodes has up-to-date data.
Read quorum defines a minimum number of nodes that have to agree on the response.
Cassandra uses version numbers to determine staleness of data.
And similar to SQL databases, we want to store copies of data across several different data centers.
For high availability.
Do you remember where else on this channel we saw practical application of a consistent hashing algorithm?
Right, when we designed distributed cache.
Please check that video if you want to know more about consistent hashing.
Another important concept to mention is consistency.
Remember that when we defined non-functional requirements we chose availability over consistency?
It simply means we prefer to show stale data than no data at all.
Let me clarify this.
Synchronous data replication is slow, we usually replicate data asynchronously.
In case of a leader-follower replication for example, some read replicas may be behind their master.
Which leads to a situation when different users see different total count for a video.
This inconsistency is temporary, over time all writes will propagate to replicas.
This effect is known as eventual consistency.
Cassandra actually extends the concept of eventual consistency by offering tunable consistency.
Let's discuss this big topic separately and in more details.
After discussing what we store and where, let's think how we can store the data.
There is a big difference how we do data modeling for SQL and NoSQL databases.
When designing data models for relational databases we usually start with defining nouns in the system.
We then convert these nouns into tables and use foreign keys to reference related data in these tables.
Let's take a look at the example.
We want to build a report that shows the following three entities: information about video, number of total views per hour for last several hours and information about the channel this video belongs to.
We pass video identifier as input for this report.
In a relational database we would define the following three tables: video info table that contains information about videos, video stats table that contains total views accumulated for each hour and channel info table that stores information about video channels.
And to generate report mentioned above, we run a JOIN query that retrieves data from all three tables.
And important property of a relational database - data is normalized.
It simply means we minimize data duplication across different tables.
For example we store video names in the video info table only.
And we do not store video names in other tables.
Because if some video name changes, we have to change it in several places in the database.
Which may lead to inconsistent data.
So, normalization is good for relational databases.
But NoSQL databases promote a different paradigm.
They say that we no longer think in terms of nouns, but in terms of queries that will be executed in the system we design.
And denormalization is perfectly normal.
Not something that we always have to do, but something that we should not be afraid of.
In Cassandra for example, report mentioned above will be logically represented as shown in the table.
We store everything required for the report together.
And instead of adding rows, as in a relational database, we keep adding columns for every next hour.
Great, we have covered the storage portion of our design.
And hopefully by now you have got the idea that both SQL and NoSQL database can be used for our solution.
What database would you chose?
Please let me know in the comments.
I also would like to clarify one thing.
As you know there are 4 types of NoSQL databases: column, document, key-value and graph.
So far we have used Cassandra as a representative of NoSQL databases.
We chose Cassandra because it is fault-tolerant, scalable (both read and write throughput increases linearly as new machines are added).
It supports multi datacenter replication and works well with time-series data.
And of course other options are available as well.
For a typical system design interview we usually do not need to know architectures of different databases.
But we need to know advantages and disadvantages of those and when to use what.
And please do not think that all NoSQL database have architectures similar to the one we discussed earlier.
Cassandra is a wide column database that supports asynchronous masterless replication.
But other NoSQL databases have different architectures.
For example MongoDB, a documented-oriented database, uses leader-based replication.
HBase, which is another column-oriented data store, similar to Cassandra, has a master-based architecture as well.
We will talk more about different database design principles on this channel.
As well as when to use each particular database type.
Ok, enough talking about databases, let's move on to data processing.
First, let's define what processing really means.
When Youtube users open some video, we want total views count for this video to be displayed immediately.
It means we need to calculate view counts on the fly, in real-time.
Also, when video owner opens statistics for the video we want to show per hour counts.
So, processing basically means we get a video view event and increment several counters: total and per hour counters.
You are in front of the whiteboard, interviewer is looking at you, ready to capture your next ideas.
Where to start?
As usual start with requirements.
Remember, we wrote them down on the whiteboard before?
We want the processing service to scale together with increase in video views.
We want to process events quickly.
And we do not want to lose data either when some processing service machine crashes or when database becomes unavailable.
So, we literally ask ourselves how to make events processing scalable, reliable and fast.
And this is another example of why knowledge and preparation are crucial for system design interviews.
Because curiosity and study will equip you with blueprints you can apply for various system designs.
Even if you never solved such problems in the past.
For example you know already that when we want to scale data processing we should think about partitioning.
When we want to avoid data loss we replicate data.
And when speed matters we should keep things in memory and minimize disk reads.
Easy, right?
But before diving into processing service detailed design, let's make sure we all agree on some basics.
The first question I have for you is whether or not we should pre-aggregate data in the processing service.
Let me clarify the question.
We have two options how to update counters in the database.
In the first option the processing service increments counter for every incoming event.
Meaning that if three users opened the same video A, the processing service simply increments total count in the database three times.
Logic is simple, event comes and we increment the counter.
In the second option, we accumulate data in the processing service memory for some period of time, lets say several seconds.
And add accumulated value to the database counter.
For example three users opened some video A, the processing service takes each event and increments in-memory counter.
And every several seconds in-memory counter value is sent to the database to calculate the final count.
I claim that the second option is better (for large scale systems of course).
Someone who agrees with me, please help me prove it.
By sharing your arguments in the comments section.
Further in this video I assume that we aggregate data in memory.
With this assumption in mind, what do you think is better: push or pull?
Where push means that some other service sends events synchronously to the processing service.
While pull means that the processing service pulls events from some temporary storage.
Although the answer is that both options are totally valid and we can make both work, pull option has more advantages, as it provides a better fault-tolerance support and easier to scale.
Let me explain.
We have two users opening two different videos A and B.
Processing service updates in-memory counters, returns successful responses back to clients and the machine crashes without sending this data to the database.
Data is lost.
The alternative to push approach is for the processing service to pull events from a storage.
Events generated by users are stored in that temporary storage first.
Processing service machine pulls events and updates in-memory counters.
And if machine crashes, we still have events in the storage and can re-process them.
And here we come to another important concept, called checkpointing.
We have a temporary storage.
And as you may see I intentionally draw it as a queue.
Because when events arrive we put them into that storage in order, one by one.
Fixed order allows us to assign an offset for each event in the storage.
This offset indicates event position in the sequence.
Events are always consumed sequentially.
Every time an event is read from the storage, the current offset moves forwards.
After we processed several events and successfully stored them in the database, we write checkpoint to some persistent storage.
If processing service machine fails, it will be replaced with another one and this new machine will resume processing where the failed machine left off.
Very important concept in stream data processing.
Another important concept is partitioning.
We already discussed it when talked about databases.
Main idea remains the same when applied to events processing.
Instead of putting all events into a single queue, let's have several queues.
Each queue is independent from the others.
Every queue physically lives on its own machine and stores a subset of all events.
For example we compute a hash based on video identifier and use this hash number to pick a queue.
As you may see partitioning allows us to parallelize events processing.
More events we get, more partitions we create.
Equipped with these basic concepts, we now ready to look deep inside the processing service.
We discussed so far that processing service reads events from partition one by one, counts events in memory, and flushes this counted values to the database periodically.
So, we need a component to read events.
The consumer establishes and maintains TCP connection with the partition to fetch data.
We can think of it as an infinite loop that polls data from the partition.
When consumer reads event it deserializes it.
Meaning it converts byte array into the actual object.
Usually, consumer is a single threaded component.
Meaning that we have a single thread that reads events.
We can implement multi-threaded access.
When several threads read from the partition in parallel.
But this approach comes with a cost, checkpointing becomes more complicated and it is hard to preserve order of events if needed.
Consumer does one more important thing - helps to eliminate duplicate events.
If the same message was submitted to the partition several times (and later you will see why this can happen), we need a mechanism to avoid double counting.
To achieve this we use a distributed cache that stores unique event identifiers for let's say last 10 minutes.
And if several identical messages arrived within a 10 minutes interval, only one of them (the first one) will be processed.
Event then comes to the component that does in-memory counting.
Let's call it aggregator.
Think of it as a hash table that accumulates data for some period of time.
Periodically, we stop writing to the current hash table and create a new one.
A new hash table keeps accumulating incoming data.
While old hash table is no longer counting any data and each counter from the old hash table is sent to the internal queue for further processing.
Why do we need this internal queue?
Why can't we send data directly to the database.
Glad you asked.
Remember, we have a single thread that reads events from the partition.
But nothing stops us from processing these events by multiple threads, to speed up processing.
Especially if processing takes time.
By sending data to the internal queue we decouple consumption and processing.
The best analogy I could think of is a security check queue at the airport.
We can have a single person that quickly checks a passport and a ticket for every passenger, but we need several lines for carry-on bags screening, as this process takes much more time.
You may argue whether we should put internal queue before Aggregator component.
It is up to you.
Both options are fine.
Ok, we now ready to send pre-aggregated values to the database.
So, we need a component responsible for this.
Database writer is either a single-threaded or a multi-threaded component.
Each thread takes a message from the internal queue and stores pre-aggregated views count in the database.
Single-threaded version makes checkpointing easier.
But multi-threaded version increases throughput.
Think about it for a moment and let me know in the comments which version you like better.
No need to worry if data flow is not completely clear to you right now, we will have a simple simulation a bit later.
It should help to further clarify the whole process.
Meanwhile, I would like to point out two more important features of the database writer.
The first concept is called a dead letter queue.
The dead-letter queue is the queue to which messages are sent if they cannot be routed to their correct destination.
Why do you think we may need one?
You are correct, to protect ourselves from database performance or availability issues.
If database becomes slow or we cannot reach database due to network issues, we simply push messages to the dead letter queue.
And there is a separate process that reads messages from this queue and sends them to the database.
This concept is widely used when you need to preserve data in case of downstream services degradation.
So, you may apply it in many system designs.
Another viable option is to store undelivered messages on a local disk of the processing service machine.
The second concept is data enrichment.
Remember how we store data in Cassandra?
We store it the way data is queried, right?
If we want for example to show video title in the report, we need to store video title together with views count.
The same is true for the channel name and many other attributes that we may want to display.
But all these attributes do not come to the processing service with every video view event.
Event contains minimum information, like video identifier and timestamp.
It does not need to contain video title or channel name or video creation date.
So, these information comes from somewhere else, right?
Some database.
But the trick here is that this database lives on the same machine as the processing service.
All these additional attributes should be retrieved from this database really quickly.
Thus, having it on the same machine eliminates a need for remote calls.
Such databases are called embedded databases.
LinkedIn for example uses this concept for the "who viewed your profile" feature.
When they show additional information about people who viewed your profile.
For example, how many viewers have recruiter job title.
One last concept I would like to mention is state management.
We keep counters in memory for some period of time.
Either in in-memory store or internal queue.
And every time we keep anything in memory we need to understand what to do when machine fails and this in-memory state is lost.
But that is easy, you may say.
We have events stored in the partition, let's just re-create the state from the point where we failed.
In other words we just re-process events one more time.
This is a good idea.
And it will work well if we store data in-memory for a relatively short period of time and state is small.
Sometimes it may be hard to re-create the state from raw events from scratch.
The solution in this case is to periodically save the entire in-memory data to a durable storage.
And new machine just re-loads this state into its memory when started.
We have looked inside the processing service.
We now ready to finalize the data ingestion pipeline.
From the moment events appear in our counting system.
We know already that we have a set of partitions and processing service reads events from them, count data in memory for some short period of time and stores total count in the database.
Someone needs to distribute data across partitions, right?
Let's have a component called Partitioner service.
Let's also have a load balancer component in front of our partitioner service.
To evenly distribute events across partitioner service machines.
When user opens a video, request goes through API Gateway, component that represents a single-entry point into a video content delivery system.
API Gateway routes client requests to backend services.
Our counting system may be one of such backend services.
And one more important component to mention is the partitioner service client.
Please prepare yourself for a lot of useful information on the next slide.
Pause this video, grab a cup of coffee or tea.
Give yourself a rest for the next 15 minutes and come back.
You will learn a ton.
I could not think of a better way then dumping all this information on you in a single shot.
Do not blame me, blame distributed systems for all the complexities they bring.
We talked about database and processing service in details.
Now let's cover remaining 3 components of the data ingestion path: partitioner service client, load balancer and partitioner service.
We will discuss many ideas these components are built upon.
And will start with some basics.
When client makes a request to a server, server processes the request and sends back a response.
The client initiates the connection by using sockets.
When a client makes a request, the socket that handles that connection on the server side is blocked.
This happens within a single execution thread.
So, the thread that handles that connection is blocked as well.
And when another client sends a request at the same time, we need to create one more thread to process that request.
This is how blocking systems work.
They create one thread per connection.
Modern multi-core machines can handle hundreds of concurrent connections each.
But let's say server starts to experience a slow down and number of active connections and threads increases.
When this happens, machines can go into a death spiral and the whole cluster of machines may die.
Remember we designed a rate limiter in one of the previous videos.
That is exactly why we need rate limiting solutions, to help keep systems stable during traffic peeks.
Alternative to blocking I/O is non-blocking I/O.
When we can use a single thread on the server side to handle multiple concurrent connections.
Server just queues the request and the actual I/O is then processed at some later point.
Piling up requests in the queue are far less expensive than piling up threads.
Non-blocking systems are more efficient and as a result has higher throughput.
You may be wondering that if non-blocking systems are so great, why we still have so many blocking systems out there?
Because everything has a price.
And the price of non-blocking systems is increased complexity of operations.
Blocking systems are easy to debug.
And this is a big deal.
In blocking systems we have a thread per request and we can easily track progress of the request by looking into the thread's stack.
Exceptions pop up the stack and it is easy to catch and handle them.
We can use thread local variables in blocking systems.
All these familiar concepts either do not work at all or work differently in the non-blocking world.
Moving on to buffering and batching.
There are thousands of video view events happening on Youtube every second.
To process all these requests, API Gateway cluster has to be big in size.
Thousands of machines.
If we then pass each individual event to the partitioner service, partitioner service cluster of machines has to be big as well.
This is not efficient.
We should somehow combine events together and send several of them in a single request to the partitioner service.
This is what batching is about.
Instead of sending each event individually, we first put events into a buffer.
We then wait up to several seconds before sending buffer's content or until batch fills up, whichever comes first.
There are many benefits of batching: it increases throughput, it helps to save on cost, request compression is more effective.
But there are drawbacks as well.
It introduces some complexity both on the client and the server side.
For example think of a scenario when partitioner service processes a batch request and several events from the batch fail, while other succeed.
Should we re-send the whole batch?
Or only failed events?
What do you think?
The next concept is timeouts.
Timeouts define how much time a client is willing to wait for a response from a server.
We have two types of timeouts: connection timeout and request timeout.
Connection timeout defines how much time a client is willing to wait for a connection to establish.
Usually this value is relatively small, tens of milliseconds.
Because we only try to establish a connection, no heavy request processing is happening just yet.
Request timeout happens when request processing takes too much time, and a client is not willing to wait any longer.
To choose a request timeout value we need to analyze latency percentiles.
For example we measure latency of 1% of the slowest requests in the system.
And set this value as a request timeout.
It means that about 1% of requests in the system will timeout.
And what should we do with these failed requests?
Let's retry them.
May be we just hit a bad server machine with the first request.
And the second attempt may hit a different server machine, increasing our chances to succeed.
But we should be smart when retry.
Because if all clients retry at the same time or do it aggressively, we may create a so-called retry storm event and overload sever with too many requests.
To prevent this, we should use exponential backoff and jitter algorithms.
Exponential backoff algorithm increases the waiting time between retries up to a maximum backoff time.
We retry requests several times, but wait a bit longer with every retry attempt.
And jitter adds randomness to retry intervals to spread out the load.
If we do not add jitter, backoff algorithm will retry requests at the same time.
And jitter helps to separate retries.
Even with exponential backoff and jitter we may still be in danger of too many retries.
For example when partitioner service is down or degraded.
And majority of requests are retried.
The Circuit Breaker pattern stops a client from repeatedly trying to execute an operation that's likely to fail.
We simply calculate how many requests have failed recently and if error threshold is exceeded we stop calling a downstream service.
Some time later, limited number of requests from the client are allowed to pass through and invoke the operation.
If these requests are successful, it's assumed that the fault that was previously causing the failure has been fixed.
We allow all requests at this point and start counting failed requests from scratch.
The loop completes.
The Circuit Breaker pattern also has drawbacks.
For example, it makes the system more difficult to test.
And it may be hard to properly set error threshold and timers.
By the way, have you noticed that everything we discussed so far has tradeoffs?
None of these concepts is a silver bullet.
This is true for almost all concepts in distributed systems.
We should always know and remember about tradeoffs.
It is hard, I agree.
More knowledge and experience you have, easier it becomes.
Let's now talk about load balancing.
It is a big topic of course, we will consider only selected concepts.
As you know load balancers distribute data traffic between multiple servers.
There are two types of load balancers: hardware and software.
Hardware load balancers are network devices we buy from known organizations.
Theses are powerful machines with many CPU cores, memory and they are optimized to handle very high throughput.
Millions of requests per second.
Software load balancer is only software that we install on hardware we choose.
We do not need big fancy machines, and many software load balancers are open source.
Load balancers provided by public clouds (for example ELB from AWS) are examples of software load balancer type as well.
Another gradation of load balancers is what traffic they serve TCP or HTTP.
It is a bit more complicated than that, but I do not want to overload you with terminology too much.
Let's keep things simple for now.
TCP load balancers simply forward network packets without inspecting the content of the packets.
Think of it as if we established a single end-to-end TCP connection between a client and a server.
This allows TCP load balancers to be super fast and handle millions of requests per second.
HTTP load balancers, on contrast, terminate the connection.
Load balancer gets an HTTP request from a client, establishes a connection to a server and sends request to this server.
HTTP load balancer can look inside a message and make a load‑balancing decision based on the content of the message.
For example based on a cookie information or a header.
Load balancers may use several algorithms to distribute the load.
Round robin algorithm distributes requests in order across the list of servers.
Least connections algorithm sends requests to the server with the lowest number of active connections.
Least response time algorithm sends requests to the server with the fastest response time.
Hash-based algorithms distribute requests based on a key we define, such as the client IP address or the request URL.
Ok, you got it, there are many benefits of using load balancers.
I should stop selling them to you.
Instead, let's return to our original system design problem and address several very specific questions.
Such as, how does our partitioner service client know about load balancer?
How does load balancer know about partitioner service machines?
And how does load balancer guarantee high availability?
Because it looks like a single point of failure, right?
Here is where we should recall DNS, Domain Name System.
DNS is like a phone book for the internet.
It maintains a directory of domain names and translate them to IP addresses.
We register our partitioner service in DNS, specify domain name, for example partitionerservice.domain.com and associate it with IP address of the load balancer device.
So, when clients hit domain name, requests are forwarded to the load balancer device.
For the load balancer to know about partitioner service machines, we need to explicitly tell the load balancer the IP address of each machine.
Both software and hardware load balancers provides API to register and unregister servers.
Load balancers need to know which server from the registered list are healthy and which are unavailable at the moment.
This way load balancers ensure that traffic is routed to healthy servers only.
Load balancer pings each server periodically and if unhealthy server is identified, load balancer stops to send traffic to it.
It will then resume routing traffic to that server when it detects that the server is healthy again.
As for high availability of load balancers, they utilize a concept of primary and secondary nodes.
The primary load balancer accepts connections and serves requests, while the secondary load balancer monitors the primary.
If, for any reason, the primary load balancer is unable to accept connections, the secondary one takes over.
Primary and secondary also live in different data centers, in case one data center goes down.
There are several other interesting topics related to load balancing, and we should definitely cover those in a separate video.
But now let's move on to the next two components of our design, partitioner service and partitions.
With partitioner service it is more or less clear.
It's a web service that gets requests from clients, looks inside each request to retrieve individual video view events (because remember we batch events on the client side), and routs each such event (we can also use the word message) to some partition.
But what partitions are?
Partitions is also a web service, that gets messages and stores them on disk in the form of the append-only log file.
So, we have a totally-ordered sequence of messages ordered by time.
This is not a single very large log file, but a set of log files of the predefined size.
Partitioner service has to use some rule, partition strategy, that defines which partition gets what messages.
A simple strategy is to calculate a hash function based on some key, let's say video identifier and chose a machine based on this hash.
This simple strategy does not work very well with large scale.
As it may lead to so called "hot partitions".
For example when we have a very popular video or set of videos and all view events for them go to the same partition.
One approach to deal with hot partitions is to include event time, for example in minutes, into partition key.
All video events within the current minute interval are forwarded to some partition.
Next minute, all events go to a different partition.
Within one minute interval a single partition gets a lot of data, but over several minutes data is spread more evenly among partitions.
Another solution to hot partitions problem is to split hot partition into two new partitions.
To get an idea how this approach might work, remember consistent hashing algorithm and how adding a new node to the consistent hashing ring splits a range of keys into two new ranges.
And if to push this idea of partition split even further, we may explicitly allocate dedicated partitions for some popular video channels.
All video view events from such channels go to their allocated partitions.
And view events from all other channels never go to those partitions.
These are the powerful techniques and there is little information on the "hot partitions" topic on the internet.
So, please remember them.
To send messages to partitions, partitioner service needs to know about every partition.
This is where the concept of service discovery comes on stage.
In the world of microservices there are two main service discovery patterns: server-side discovery and client-side discovery.
We already looked at server-side discovery when talked about load balancers.
Clients know about load balancer, load balancer knows about server-side instances.
Easy.
But we do not need a load balancer between partitioner service and partitions.
Partitioner service itself acts like a load balancer by distributing events over partitions.
This is a perfect match for the client-side discovery pattern.
With client-side discovery every server instance registers itself in some common place, named service registry.
Service registry is another highly available web service, which can perform health checks to determine health of each registered instance.
Clients then query service registry and obtain a list of available servers.
Example of such registry service is Zookeeper.
In our case each partition registers itself in Zookeeper, while every partitioner service instance queries Zookeeper for the list of partitions.
Do you remember where else we discussed client-side service discovery pattern, although we did not name it there that way?
When we talked about distributed cache design.
When cache client needs to pick a cache shard that stores the data.
There we discussed several other options as well.
Please go and check that video.
One more option for service discovery is similar to what Cassandra does.
Remember we mentioned before that Cassandra nodes talk to each other?
So, every node in the cluster knows about other nodes.
It means clients only need to contact one node from the server cluster to figure out information about the whole cluster.
Think about this.
Next important concept is replication.
We must not lose events when store them in partitions.
So, when event is persisted in a partition, we need to replicate it.
If this partition machine goes down, events are not lost.
There are three main approaches to replication: single leader replication, multi leader replication and leaderless replication.
Do you remember where we used single leader replication?
Correct, when we discussed how to scale a SQL database.
Great, and do you remember when we talked about leaderless replication?
When we discussed how Cassandra works, right?
So far we did not talk about multi leader replication.
Let me make a separate deep dive into replication topic.
And only mention right now that multi leader replication is mostly used to replicate between several data centers.
So, which approach should we chose for partitions?
Let's go with single leader replication.
Each partition will have a leader and several followers.
We always write events and read them from the leader only.
While a leader stays alive, all followers copy events from their leader.
And if the leader dies, we choose a new leader from its followers.
The leader keeps track of its followers: checks whether the followers are alive and whether any of the followers is too far behind.
If a follower dies, gets stuck, or falls behind, the leader will remove it from the list of its followers.
Remember a concept of a quorum write in Cassandra?
We consider a write to be successful, when predefined number of replicas acknowledge the write.
Similar concept applies to partitions.
When partitioner service makes a call to a partition, we may send response back as soon as leader partition persisted the message, or only when message was replicated to a specified number of replicas.
When we write to a leader only, we may still lose data if leader goes down before replication really happened.
When we wait for the replication to complete, we increase durability of the system, but latency will increase.
Plus, if required number of replicas is not available at the moment, availability will suffer.
Tradeoffs, as usual.
Next topic is the last one on this slide, I promise.
Let's talk about message formats.
We can use either textual or binary formats for messages.
Popular textual formats are XML, CSV, JSON.
Popular binary formats are Thrift, Protocol Buffers and Avro.
What's great about textual formats - they are human-readable.
They are well-known, widely supported and heavily used by many distributed systems.
But for the large scale real-time processing systems binary formats provide much more benefits.
Messages in binary format are more compact and faster to parse.
And why is this?
As mentioned before, messages contain several attributes, such as video identifier, timestamp, user related information.
When represented in JSON format, for example, every message contains field names, which greatly increases total message size.
Binary formats are smarter.
Formats we mentioned before require a schema.
And when schema is defined we no longer need to keep field names.
For example Apache Thrift and Protocol Buffers use field tags instead of field names.
Tags are just numbers and they act like aliases for fields.
Tags occupy less space when encoded.
Schemas are crucial for binary formats.
Message producers (or clients) need to know the schema to serialize the data.
Message consumers (processing service in our case) require the schema to deserialize the message.
So, schemas are usually stored in some shared database where both producers and consumers can retrieve them.
Important to mention that schemas may and will change over time.
We may want to add more attributes into messages and use them later for counting or filtering.
Apache Avro is a good choice for our counting system.
That was tough.
Talking about all these concepts completed our discussion of the data ingestion path.
And all the most difficult stuff is behind us.
Do not worry if some mentioned before concepts are not completely clear to you right now.
Each of them deserves a video on its own.
And we will talk more about them on this channel.
Eventually, you will feel comfortable using all of them, either on the interview or in your day to day job.
Now let's take a look at data retrieval path.
When users open a video on Youtube, we need to show total views count for this video.
To build a video web page, several web services are called.
A web service that retrieves information about the video, a web service that retrieves comments, another one for recommendations.
Among them there is our Query web service that is responsible for video statistics.
All these web services are typically hidden behind an API Gateway service, a single-entry point.
API Gateway routes client requests to backend services.
So, get total views count request comes to the Query service.
We can retrieve the total count number directly from the database.
Remember we discussed before how both SQL and NoSQL databases scale for reads.
But total views count scenario is probably the simplest one.
This is just a single value in the database per video.
The more interesting use case is when users retrieve time-series data, which is a sequence of data points ordered in time.
For example, when channel owner wants to see statistics for her videos.
As discussed before, we aggregate data in the database per some time interval, let's say per hour.
Every hour for every video.
That is a lot of data, right?
And it grows over time.
Fortunately, this is not a new problem and solution is known.
Monitoring systems, for example, aggregate data for every 1 minute interval or even 1 second.
You can imaging how huge those data sets can be.
So, we cannot afford storing time series data at this low granularity for a long period of time.
The solution to this problem is to rollup the data.
For example, we store per minute count for several days.
After let's say one week, per minute data is aggregated into per hour data.
And we store per hour count for several months.
Then we rollup counts even further and data that is older than let's say 3 months, is stored with 1 day granularity.
And the trick here is that we do not need to store old data in the database.
We keep data for the last several days in the database, but the older data can be stored somewhere else, for example, object storage like AWS S3.
In the industry, you may also hear terms like a hot storage and a cold storage.
Hot storage represents frequently used data that must be accessed fast.
Cold storage doesn’t require fast access.
It mostly represents archived and infrequently accessed data.
When request comes to the Query service, it does so-called data federation, when it may need to call several storages to fulfill the request.
Most recent statistics is retrieved from the database, while older statistics is retrieved from the Object Storage.
Query service then stitches the data.
And this is ideal use case for the cache.
We should store query results in a distributed cache.
This helps to further improve performance of queries and scale them.
We covered both data ingestion and data retrieval.
Not many things left.
Let me show you the full picture and share with you several other important topics.
Three users opened some video A.
And API Gateway got 3 requests.
Partitioner service client batches all three events and sends them in a single request to the partitioner service.
This request hits the load balancer first.
And load balancer routes it to one of the partitioner service machines.
Partitioner service gets all three events from the request and sends them to some partition.
All three events end up in the same partition, as we partition data based on the video identifier.
Here is where processing service appears on the stage.
Partition consumer reads all three messages from the partition one by one and sends them to the aggregator.
Aggregator counts messages for a one minute period and flushes calculated values to the internal queue at the end of that minute.
Database writer picks count from the internal queue and sends it to the database.
In the database we store count per hour and the total number of views for each video.
So, we just add a one minute value to the current hour count as well as the total count.
Total count was 7 prior to this minute and we add 3 for the current minute.
And during data retrieval, when user opens video A, API Gateway sends request to the Query service.
Query service checks the cache.
And if data is not found in the cache, or cache value has expired, we call the database.
Total count value is then stored in the cache and Query service returns the total count back to the user.
I hope that this simulation helped you further understand the meaning of each component in the architecture.
Feel free to post any questions you have in the comments section.
Another important aspect of an interview and system design in general is a technology stack.
When we design some system, we usually do not need to reinvent the wheel.
We rely on some well-regarded technologies.
Either open source or commercial.
Public cloud services.
During the interview do not forget to discuss these technologies.
You may do this along the way or at the end of the interview.
So, let's see what technologies we may use for our solution.
Netty is a high-performance non-blocking IO framework for developing network applications, both clients and servers.
Frameworks such as Hystrix from Netflix and Polly simplify implementation of many client-side concepts we discussed before: timeouts, retries, circuit breaker pattern.
Citrix Netscaler is probably the most famous hardware load balancer.
Among software load balancers NGINX is a very popular choice.
And if we run our counting system in the cloud, for example Amazon cloud, then Elastic Load Balancer is a good pick.
Instead of using our custom Partitioner service and partitions, we could use Apache Kafka instead.
Or Kafka's public cloud counterpart, like Amazon Kinesis.
To process events and aggregate them in memory we can use stream-processing frameworks such as Apache Spark or Flink.
Or cloud-based solutions, such as Kinesis Data Analytics.
We already talked about Apache Cassandra.
Another popular choice for storing time-series data is Apache HBase database.
These are wide column databases.
There are also databases optimized for handling time series data, like InfluxDB.
We also mentioned before that we may need to store raw events to recalculate counts in case of any error or if customers need to run ad-hoc queries.
We can store raw events in Apache Hadoop or in a cloud data warehouse, such as AWS Redshift.
And when we roll up the data and need to archive it, AWS S3 is a natural choice.
I would like to also mention several other important technologies we may use in our design.
Vitess is a database solution for scaling and managing large clusters of MySQL instances.
Vitess has been serving all Youtube database traffic since 2011.
In several places of our design we rely on a distributed cache: for message deduplication and to scale read data queries.
Redis is a good option.
For a dead-letter queue mechanism, when we need to temporarily queue undelivered messages, we may use an open-source message-broker such as RabbitMQ.
Or public cloud alternative, such as Amazon SQS.
For data enrichment, when we store video and channel related information locally on the machine and inject this information in real-time, we may use RocksDB, a high performance embedded database for key-value data.
To do leader election for partitions and to manage service discovery, we may rely on Apache Zookeeper, which is a distributed configuration service.
For the service discovery piece we actually have an alternative, Eureka web service from Netflix.
To monitor each of our system design components we may rely on monitoring solutions provided by public cloud services, such as AWS CloudWatch.
Or use a popular stack of open source frameworks: Elasticsearch, Logstash, Kibana.
Or ELK for short.
We discussed before that binary message format is preferred for our system.
Popular choices are Thrift, Protobuf and Avro.
For Partitioner service to partition the data, we should use a good hashing function, for example a MurmurHash.
We are done with the detailed system design.
And here is where our interviewer will start challenging us with the choices we have made.
There are several goals of this exercise.
The interviewer wants to see that we know and understand tradeoffs.
Have you noticed that I usually use verbs like may or can and rarely use must or have to?
This is because we usually have several options to choose from.
When we design a system or a part of it in real life, we usually bring several options to discuss with the team, right?
And very important is not only know your options, but be able to explain pros and cons of each one.
We discussed many tradeoffs of individual components throughout this video.
Let's see what else the interviewer may want to discuss with us.
To identify bottlenecks in the system we need to test it under a heavy load.
This is what performance testing is about.
There are several types of performance testing.
We have load testing, when we measure behavior of a system under a specific expected load.
We have stress testing, when we test beyond normal operational capacity, often to a breaking point.
We have soak testing, when we test a system with a typical production load for an extended period of time.
With load testing we want to understand that our system is indeed scalable and can handle a load we expect.
For example, a two or three times increase in traffic.
With stress testing we want to identify a breaking point in the system.
Which component will start to suffer first.
And what resource it will be: memory, CPU, network, disk IO.
And with soak testing we want to find leaks in resources.
For example, memory leaks.
So, generating high load is the key.
Tools like Apache JMeter can be used to generate a desired load.
Health monitoring.
All the components of our system must be instrumented with monitoring of their health.
Metrics, dashboards and alerts should be our friends all the time.
Metric is a variable that we measure, like error count or processing time.
Dashboard provides a summary view of a service’s core metrics.
And alert is a notification sent to service owners in a reaction to some issue happening in the service.
Remember about the four golden signals of monitoring, which are latency, traffic, errors, and saturation.
Let's leave details for a separate video.
Ok, we designed a system and deployed all the components.
We know it is running healthy and can handle a high load.
But how to make sure it counts things correctly?
This becomes critical when we not just count video views, but, for example, number of times some ad was played in a video.
As we need to properly charge an ad owner and pay money to a video owner.
This problem is typically addressed by building an audit system.
There can be two flavors of audit systems.
Let's call them weak and strong.
Weak audit system is a continuosly running end-to-ed test.
When let's say once a minute we generate several video view events in the system, call query service and validate that returned value equals to the expected count.
This simple test gives us a high confidence that the system counts correctly.
And it is easy to implement and maintain such test.
But unfortunately, this test is not 100% reliable.
What if our system loses events in some rare scenarios?
And weak audit test may not identify this issue for a long period of time.
That is why we may need a better approach.
Strong audit system calculates video views using a completely different path then out main system.
For example we store raw events in Hadoop and use MapReduce to count events.
And then compare results of both systems.
Having two different systems doing almost the same may seem like an overkill, right?
You may be surprised but this is not so uncommon in practice.
Not such a long time ago it was quite a popular idea.
And it even has a name - Lambda Architecture.
The key idea is to send events to a batch system and a stream processing system in parallel.
And stitch together the results from both systems at query time.
You can get a better understanding of this idea if you watch the previous video on the channel, where we designed a system for finding the top k most frequent items.
Ideally, we should have a single system.
Let me share with you advice from Jay Kreps, who is one of the authors of Apache Kafka.
We should use a batch processing framework like MapReduce if we aren’t latency sensitive, and use a stream processing framework if we are, but not to try to do both at the same time unless we absolutely must.
And please note that out today's problem can indeed be solved with MapReduce.
But MapReduce-based system would have a much higher latency.
We already discussed the problem with popular videos.
I will just reiterate the key idea.
We have to spread events coming for a popular video across several partitions.
Otherwise, a single consumer of a single "hot" partition may not be able to keep up with the load.
And will fall behind.
Let's talk more about this.
Imaging a situation when the processing service cannot keep up with the load.
Maybe because number of events is huge, maybe because processing of a single event is complicated and time consuming.
I will not dive too much into details, but describe the main idea of the solution.
We batch events and store them in the Object Storage service, for example AWS S3.
Every time we persist a batch of events, we send a message to a message broker.
For example SQS.
Then we have a big cluster of machines, for example EC2, that retrieve messages from SQS, read a corresponding batch of events from S3 and process each event.
This approach is a bit slower than stream processing, but faster than batch processing.
Everything is a tradeoff.
Let's summarize what we have discussed.
We start with requirements clarification.
And more specifically, we need to define APIs, what exactly our system is supposed to do.
We then discuss non-functional requirements with the interviewer and figure out what qualities of the system she is most interested in.
We can now outline a high-level architecture of the system.
Draw some key components on the whiteboard.
At the next stage we should dive deep into several of those components.
Our interviewer will help us understand what components we should focus on.
And the last important step is to discuss bottlenecks and how to deal with them.
And let me quickly remind you some specifics we discussed for each of these steps.
To define APIs, we discuss with the interviewer what specific behaviors or functions of the system we need to design.
We write down verbs characterizing these functions and start thinking about input parameters and return values.
We then can make several iterations to brush up the APIs.
After this step we should be clear on what the scope of the design is.
To define non-functional requirements, just know what your options are.
Open a list of non-functional requirements on wiki and read the list.
There are many of them.
I recommend to focus on scalability, availability and performance.
Among other popular choices we have consistency, durability, maintainability and cost.
Try to pick not more than 3 qualities.
To outline a high-level design, think about how data gets into the system, how it gets out of the system and where data is stored inside the system.
Draw these components on the whiteboard.
It is ok to be rather generic at this stage.
Details will follow later.
And although it is not easy, try to drive the conversation.
Our goal here is to get understanding of what components to focus on next.
And the interviewer will help us.
While designing specific components, start with data.
How it is stored, transferred and processed.
Here is where our knowledge and experience becomes critical.
By using fundamental concepts of system design and by knowing how to combine these concepts together, we can make small incremental improvements.
And apply relevant technologies along the way.
After technical details are discussed, we can move to discussing other important aspects of the system.
Listen carefully to the interviewer.
She sees bottlenecks of our design and in her questions there will be hints what those bottlenecks are.
And what can really help us here is the knowledge of different tradeoffs in system design.
We just need to pick and apply a proper one.
Today we covered a big topic.
If you are still with me watching this video you should be proud of yourself.
Seriously.
There were many system design concepts covered in the video.
And I hope you have a better understanding right now why I consider knowledge the key to the successful system design interview.
And system design in general.
And although we talked about a specific problem today, like video views counting, the same ideas can be applied to other problems, for example counting likes, shares, reposts, ad impressions and clicks.
The same ideas can be applied to designing monitoring systems, when we count metrics.
When we design a fraud prevention system we need to count number of times each credit card was used recently.
When we design recommendation service we may use counts as input to machine learning models.
When we design "what's trending" service, we count all sorts of different reactions: views, re-tweets, comments, likes.
And many other applications.
There are plenty of other important system design concepts we have not covered today.
As it is practically impossible to do in a single video.
But we will have them covered in other videos on this channel.
Thank you for being with me and I will see you next time.
Bye.
