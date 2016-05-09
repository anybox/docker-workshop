# Overpower volumes


* How can I do to manage persistent data ? As each time I remove a container
  I'm losing it but I expected to update my application without loosing data!

* Does I need to rebuild my image to test my application each time? this is time
  consuming.

* What is the plan to backup an applications? ...

* ...

We will see some examples then some theories about docker storage.

Examples are stored in [docker workshop example project](https://github.com/
anybox/docker-workshop-example/tree/master/02_volumes "Volumes examples")
where you will learn how to use:

* Volume declaration in Dockerfile or at Runtime
* Share volumes between containers
* Map host volumes

Then see what is behind the scene [Storage consideration](storage.md)
