    High level approach
Beginning the project, we knew as a group that our biggest struggle would be our unfamiliarity with html and HTTPS 
syntax and how the concepts applied to our code. Once we understood how to send a request correctly we began setting up 
the structure of our code. The first thing we prepared was for how long our code would run. We knew that once the 
crawling began we would want to stop once we found and recorded all 5 flags. So we started by putting our code in a 
while loop that ran while the length of a global secret flags list was less than 5. Another preparation we made was 
making two lists, one for where we need to crawl, and one that will hold what we have already crawled. Having these, we
 could keep track of what the code needs to explore next as well as making sure we don't visit pages more than once. 
To go through the html responses we received, we created our own html parser using the html parser library. To create 
this parser, we made a htmlparser class with functions to parse html headers and data. Using this parser we were able 
to easily extract the paths to the pages we need to crawl and the data of htmls that contain the secret flags. Once we 
had this setup, implementing the functionality was the easiest part. After all the parsing all we had to do was set up 
the format of our requests and insert the next page we wabt to crawl, check for flags and more places to crawl, and move
 on.
    
    Challenges
One of our biggest challenge was not being able to log in. We did not realize that we needed the csrfmiddleware value as
well as the csrf and sessionid cookies. We had to learn how to format POST and GET messages properly as we spent a lot of
time reformatting these requests so that they would work as intended. We also had struggled with error catching all the error
messages that the website produced. For example, we weren't accounting for the random 503 errors, and this would cause us to not find
some flags. We also tried increasing the performance using multi-threading, but it did not end up working so we increased the 
performance using one while loop rather multiple loops with in the loop.

 


    Testing
We tested our code using print statements to specifically test that the crawler was crawling through the data as intended as was not 
stuck in any loops. We also used print statements to see the value of the flags to see if the program was finding the flags correctly.
We used a counter to see how fast out program would crawl through the web pages, and would use this information to make our program more 
efficent. 