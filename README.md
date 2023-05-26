# Twitter_Clone
                           

## Implementation Details

This project aims to implement basic functionality similar to Twitter. The architecture follows the client-server model commonly used in web-based services. Instead of using a database, runtime memory is utilized.

The following files serve specific functionalities:

### Mainclass.erl
This file acts as an interface to the user, buffering communication between the client and server. It constantly listens for messages from any process.

### Sendreceive.erl
This file handles various functionalities, including sending and receiving tweets, printing tweets on the console, and managing different types of tweets such as those belonging to specific hashtags or users.

### Register.erl
This file focuses on user-specific actions such as registration, sign in, sign out, and maintaining a subscription list for each user. It also provides functionality to verify the correctness of a given username and password.

### Automation.erl
This file contains functions that automate processes such as registration and subscription. It is primarily used for simulating testers.

In this project, Erlang maps are extensively used for storing information. They offer easy accessibility and have constant time complexity (O(1)) for storing and retrieving data. Persistent terms are utilized for storing certain variables to avoid passing them around in functions repeatedly.

## Flow of the Code

1. First, call the `startTwitter` function. This function starts all the essential processes in the Twitter application. Once that is done, the server will be up and running.

2. Call `startTheRegistration()` to register a user. Then, call the same method to sign in. After signing in, users can perform various operations using `mainclass.erl` as the interface file.

## Zipf Distribution

To implement the Zipf distribution, we establish a correlation between the number of subscribers to a user and the number of tweets a user has posted. The correlation is such that the number of tweets is directly proportional to the number of subscribers. In other words, as the number of subscribers increases, so should the number of tweets.

We have implemented this correlation in the following way: the user with the most subscribers (let's say 'k') has 'k' tweets, the user with the next most subscribers has 'k/2' tweets, and so on. We follow this specific distribution to satisfy the 'f=c/x' property of Zipf.

## Max Users

We were able to simulate 100k users. While it is possible to simulate more, it takes a significant amount of time to complete the simulation. We observed that using maps for data storage is an efficient approach. When we replaced it with lists, we were unable to obtain the output even for 10k users.

## Connection, Disconnection, and Retweets

We implemented periods of connection and disconnections by using a map that keeps track of the users who are signed in. Live messages are sent only to the signed-in users. If a user signs out, their process ID is removed from the map. For retweets, we simply append the original tweet with "Retweeted" and send it as the original tweet from a user.

Example:
User 1: Hi
User 2: Retweeted User: Hi

## Performance Metrics

In our graphs, we observed that as the number of users increases, there is a sharp increase in the time taken. Additionally, with an increase in the number of subscribers, there is a significant increase in the time taken, as tweet distribution becomes more complex with a growing number of subscribers.

## How to Run

1. Replace `VenkatsaiROGG15` in "centralserver@VenkatsaiROGG15" with your own host name in all the files.
2. Compile the following files:
   - mainclass.erl
   - automation.erl
   - register.erl
   - sendreceive.erl
3. Start the first command prompt as follows: `erl -sname centralserver`
4. In that command prompt, enter the command `mainclass:startTwitter()`.
5. For simulation purposes, in the second command prompt, enter the command `automation:startAutomation()` and specify the number of users and the number of disconnected users you want in the simulation.
6. For perspective use, in the second command prompt, enter the command `mainclass:startTheRegistration()`. Register a user and sign in using the same command. After that, perform various operations using `mainclass` as the interface.


