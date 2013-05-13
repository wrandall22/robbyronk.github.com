# N-Tier Applications at Cru
###### Specializing in Layers, Not Applications

Our team has been talking about this and I thought it deserved some more thought and writing down. 

## The Layers
Each of the layers should have strictly defined interfaces and should only interact with the adjacent layers.

From user down:
- Front End
  - View
  - Application Logic
  - Service Layer
  - REST Client
- Back End
  - REST Server
  - Auth Layer
  - Business Logic
  - Data Transformation
  - Database Client
  - Database

### Front End

#### View
The View is the HTML templates. It only communicates with the Application Logic (applog) layer. The interface between applog and view is $scope.

The View should:
- Format data using filters
- Call functions on $scope
- Present data from $scope

The View should not:
- Transform data into more data

#### Applcation Logic
Think Angular controllers. The Application Logic (applog) layer exposes data and functions on the scope. Applog injects services from the service layer.

Applog should:
- Put data and functions on $scope
- Provide promises to the view
- Consume promises from services

Applog should not:
- Extensively transform or aggregate data
- Format data
- Use $http or $resource
- Have any notion of what HTTP is

#### Service Layer
This layer isn't always needed in trivial apps. Non-trivial data transformations should have automated tests and above average code coverage. 

Interface: provide promises to the Application Logic layer, consume promises from the REST Client and other services

Service Layer should:
- Contain any extensive Client Side transformations or aggregations of data
- DRY up the applog layer

Service Layer should not:
- Use $http or $resource

#### REST Client
This layer of services is the only one that should inject $http or $resource.

Interface: provide promises to the service layer, issue HTTP requests to the server.

REST Client should:
- Use $http or $resource
- Abstract away HTTP details
- Transmogrify JSON into POJSOs

REST Client should not:
- Leak HTTP details up

--------------

### Back End

#### REST Server
Interface: HTTP Responses to the REST Client. Uses methods on business logic objects.

REST Server should:
- Abstract away HTTP details
- Transmogrify POJOs into JSON

REST Server should not:
- Contain Business Logic, Authentication or Authorization
- Leak HTTP details down

#### Authentication and Authorization
Authentication should use OAuth. Authorization should use @mattdrees new framework which he proposes [here](https://gist.github.com/mattdrees/5532475).

Auth should:
- Handle all external security

Auth should not:
- Deal with HTTP

#### Business Logic
With all the business logic inside of Plain Old Java Objects, the code is portable between frameworks and testable without a Java EE container. Data transformation should only happen when Business Logic drives the transformation. This layer deserves very high code coverage. Be sure to consider error cases.

Business Logic Layer should:
- Testable by plain vanilla JUnit/TestNG/whatever
- Contains all the business logic

Business Logic Layer should not:
- Transform data to enable BizLog

#### Data Transformation
This layer exists to do data transformations between the Business Logic and the Database Client layers, making these layers smaller. This layer should be testable without a Java EE container. Moving data transformations out of the hard-to-test database client layer and into the easy-to-test transformation layer will reduce maintenance costs. Moving data transformations out of the high coverage BizLog layer and into the less-than-high coverage transformation layer will increase agility.

Data Transformation Layer should:
- Transform data to enable Business Logic
- Transform data to simplify the Database Client
- Testable by plain vanilla JUnit/TestNG/whatever

Data Transformation Layer should not:
- Contain any Business Logic
- Have a clue about what database is underneath
- Have 100% code coverage

#### Database Client
Whether it's Mongo, Riak, Redis, Postgres or even Oracle, this is the layer that cares about what the database is.

Database Client should:
- Issue the queries to the database
- Contain any `@Entity` objects
- Handle failover database connections

Database Client should not:
- Leak DB exceptions or details upward

#### Database

Database should:
- Store stuff

Database should not:
- Have any business logic unless you have performance needs and proof that the DB is more performant
