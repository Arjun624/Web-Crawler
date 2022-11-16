
1. High level approach
Attacking this project we quickly discovered that we had to be careful not to dig ourselves too deep into a hole. For 
example after finishing tests two and moving to test 3 we quickly found that hard coding window size was making one 
test fail and the other pass. Keeping this in mind we decided to run through all the tests strategies in the 
implementation suggestions and map out our code in a way that we try and keep all the factors we needed in the future 
in mind. After mapping these things out like making sure we don't succeed on a test based on randomly changing the RTO 
or window size, we started looking into some of the strategies that real TCP programs used. We decided very early that 
the idea of fast retransmit and duplicate acknowledgements suited our implementation. We saw that we could make our 
recv fire out tons of acknowledgements at a time and to keep up with our send sending a window of packets to it. We used
this to implement a fast retransmit type of packet loss system. As we approached the latency and bandwidth tests we 
saw that this fast retransmission was often so fast that we were filling the router and sending many extra packets that 
were going nowhere. We decided to really flesh out and think deeply on our RTT and decided to increase the timeout of 
our recv based on how many duplicates we were sending. If we send enough to the send server to let it know it needs to 
retransmit, we could give it a break and allow it some time to retransmit by increasing the time-out in our select to 
half to 300% of our base time out which was closer to half of the normal RTT of 1 second. If send was keeping up with 
recv then we would set the time-out back to the lower base value to encourage the fast interactions. This created a 
give and take with our programs allowing them to stay efficient. This interaction was then linked when moving to the 
level 7 tests. The window sized decreased when the programs were not synced up and increased when they could handle 
higher levels of transmissions. Taking a step back and picturing these interactions really helped us as we could really 
visualize this perfect area that we had to get our code to reach where it sent and received the perfect amount of 
packets. Knowing we always had to return to this spot after fixing bugs became easier.
    
2. Challenges
One of the biggest challenges we faced was to keep our other functionalities working while we added new functionality to 
our transport protocol. When implementing new functionality we had frequently seen how previous functionality hindered 
progress. To progress in this project we had to work through chunks rather than step by step. Add functionality test 
it, then walk backwards through the project confirming previous functionality and efficiency as well as making sure we 
were not doing anything that would not allow expansion later. The tests were very successful at shining light on 
shortcuts and lack of foresight. They were prepared for us to make changes with hard coding solution to other tests that 
we were supposed to base on the environment of the transfer. Finding right window sizes and RTO times were great 
examples of big challenges as many hard coded combinations work for different tests, but we had to plan out and 
deduce smart ways for our code to figure out these values in the process of the transfer to really succeed. 

3. Properties/Features
- Fast retransmit
- Duplicate packet detection using fast retransmit 
- Packet loss detection by checking RTT time and duplicate acknowledgements
- Packet corruption detection using hashing algorithms and catching exceptions
- Packet reordering detection using a window like placeholder in the recv to negate false packet loss flagging
- Packet out of order detection when we receive the right packets at the wrong time
- Smart acknowledgements that contained sequence number and never sent the incorrect ack
- Double confirmation of completion to correct early terminations


4. Testing
We tested our code using the provided tests. We also tested our code using logs to make sure that we were sending the
correct packets and receiving the correct packets. We realized to that logs are more accurated than print statements. 
We also tested our code using the times that were outputted when you ran the tests. We would then edit our code and 
compare the times to make sure that we were improving the times. We used the 
./test script to run all the previous tests and make sure that we were not breaking any of the previous tests.