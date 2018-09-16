# Selenium Grid
Created Saturday 15 September 2018

Grid Benefits
-------------
Selenium grid is a proxy server that runs tests against a remote browser instance.
This helps in distributing the load of testing accross several servers
Allows multiple configurations of the tests to be run accross different browsers platforms and devices all at the same time

### Components to the grid:

1. **Hub:**
	a. Central server for the grid
	b. Point where tests are executed
	c. Hub is launched on a single machineand connects to 1 or more nodes regstered to it.
	d. Can only be 1 hub in a Grid instance
2. **Node:**
	a. Servers registered to the bug
	b. Receive test scripts from the hub and run them
	c. Need not be same platform as the hub
	d. Many nides registered to a hub in a grid instance


### Hub and Node Relationship works:

* Test Executed on the hub
* Hub searches through the registered nodes based on criteria
* If a matching node is found the hub sends test scripts to that node


Say we want to run a test on the hub creating a remote Firefox driver, hub will search through all available nodes to see which one has firefox
If multiple nodes available then first available node is chosen.

Thus smart routing between hub and node.
Allows many tests to be run concurrently
Manages multiple connections simultaneously
Thus grid is great for scaling infrastructure but requires setup and maintainence of both hub and nodes

Setting up the hub
------------------
We need to download the selenium stand alone server (jar) with grid support from seleniumhq

To start the server : ``java -jar selenium-server-standalone-3.14.0.jar -role hub``

Later goto <http://localhost:4444/grid/console> to see the config of the hub

Configuring nodes
-----------------
Once hub is setup now a node is required
To Register a node : ``java -jar selenium-server-standalone-3.14.0.jar -role node -hub http://localhost:4444/grid/register``
note that for registering different machine as node we need to replace localhost with the public ip address of the hub machine.

Terminal output will mention if registration was successful.
Later goto the hub console, you should see how many browser instances are available for concurrent use.
Customization is available for the node

Here testing is done on a single local node but that will not be the real-world scenario.

### Configuring many nodes
Each node server must have;

1. Standalone server
2. Browsers to run tests against
3. Locations of the hub registration endpoint


Running tests
-------------
Lets try to run against a GRID
Now in code we need to change our code to adjust to the grid i.e. :``remote , desired_capabilities: :firefox``
Funtionality is the same as normal selenium tests only difference was that it went via the Grid
Additional Details can be displayed in the console output

### Now we need to consider the following:

* **Where and how to maintain infrastructure:** For the current, single hub and local node config we can only use it for testing
* **Physical vs virtual servers**


Pros & Cons
-----------
Using Grid is great as it solve the problem of running tests accross many platforms and browsers in a nice delegated distribution
| Pros                                                                                                             | Cons                                                                                                                                                         |
|:-----------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| It can Scale well by distributing tests on several machines and running it in parallel                           | Requires maintainence to keep the hub and node running smothly<br>Thus enable warning and logs for easy debugging<br>Create scipts for managing nodes        |
| It is a central way to manage multiple environments<br>Thus runs against a large combination of browsers and OSs | Its possible that performance will start to degrade over time<br> best to explicitly kill browser after each tests<br>Restart the nodes/servers periodically |
| It can find specified nodes quickly and easily<br>Routes test scripts to the correct node                        |                                                                                                                                                              |


