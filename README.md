# am-digital-challenge

This is the response to The Asset Management Digital Challenge developed by Rafael Banzo

## Comments about the implementation

In the development HATEOAS (Hypertext As The Engine Of Application State) has been used.
In my opinion, its main advantage is that it allows the client to navigate easily through the provided links.

The operations exposed by the REST API are:
-nearestShop (GET)
-->receives longitude and latitude as parameters
-->returns the nearest shop
-shop (GET)
-->receives the name of the shop as a parameter
-->returns the shop
-shop (PUT)
-->receives a JSON Shop as parameter
-->returns a JSON containing the inserted shop and the previous shop with the same name (if any)

The location of the coordinates of the Postcode has been done using google-maps-services.
Using this the integration has been easy as this API exposed even methods to make asynchronous calls.
The asynchronous calls have been used so that the response to the put operation is fast.
The user does not need to receive the postcode in the response and it is update asynchronously.

The data is kept in memory using a ConcurrentHashMap.
An object of this class has been used because:
-the previous value is returned in the put method
-it is thread safe
-it supports full concurrency of retrievals and
-high expected concurrency for updates. This class obeys the

Three layers have been used in the design:
-Controller: receives the URL parameters or JSON, calls the service and prepares the JSON for the response
-Service: handdles the logic
-Repository: stores the data


### Prerequisites

It is necessary to have gradle configured in the machine.


### Installing

1. Download the code
First clone the git repository from https://github.com/rafaelbanzo/am-digital-challenge/
2. Build the jar and run tests
gradlew build
3. Run the springboot application
java -jar build/libs/am-digital-challenge-1.0.0.jar

## Running the tests

There are three types of tests:

-An example of a unit test ShopPseudoRepositoryTest.java
In this test, the pseudo repository where the data is kept is tested.
At the moment, only the create functionality is tested.

-An example of integration test ShopIntegrationTests.java
In this test, two shops whit the same name are submitted at the same time.
The test checks that the number is correct in each response.
It also checks that there is one and only one response with the information of the updated shop

-The Postman tests used to deploy the application.
The postman test are in the postman directory. 
They have to be imported to postman in order to run them.
They connect to localhost on port 8080.


While building the jar, the junit and integration tests are automatically run.

## How you would expand this solution, given a longer development period?
I would store the API_KEY of google maps in a properties file.  
I would handle the possible errors better.  
I would store the shops in a database, ensuring that the updating and concurrency requirements are met.

## How would you go about testing this solution?
At the moment I have writing some postman tests.  
Anyway, I think that the best approach to testing this project would be to write behavioural test using, for instance, Cucumber.

## How would you integrate this solution into an existing collection of solutions used by the Retail Manager?
It would depend on how the existing solutions had been implemented.

## How would you go about deploying this solution to production systems?
I would run the application inside docker containers.


## Authors

* **Rafael.Banzo@gft.com **




