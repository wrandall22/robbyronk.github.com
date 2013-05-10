# N-Tier Applications at Cru
###### Specializing in Layers, Not Applications

Our team has been talking about this and I thought it deserved some more thought and writing down.

## The Layers

From user down:
- View
- Application Logic
- Service Layer
- REST Client
- REST Server
- Business Logic
- Data Transformation
- Database Client
- Database

### View
The View is the HTML templates. It only communicates with the Application Logic (applog) layer. The interface between applog and view is $scope.

The View should:
- Format data using filters
- Call functions on $scope
- Present data from $scope

The View should not:
- Transform data into more data
- Have knowledge of anything below applog

### Applcation Logic
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

### Service Layer
This layer isn't always needed in trivial apps.

Interface: provide promises to the Application Logic layer, consume promises from the REST Client and other services

Service Layer should:
- Contain any extensive Client Side transformations or aggregations of data
- DRY up the applog layer

Service Layer should not:
- Use $http or $resource

### REST Client
Interface: provide promises to the service layer, HTTP requests to the server.

REST Client should:
- Use $http or $resource
- Abstract away HTTP details

REST Client should not:
- Leak HTTP details up


--------------
#### :arrow_up: Client Side/Front End
#### :arrow_up_down: HTTP
#### :arrow_down: Server Side/Back End
--------------

### REST Server
Interface: HTTP Responses to the REST Client. Uses methods on business logic objects.

REST Server should:
- Abstract away HTTP details

REST Server should not:
- Contain Business Logic, Authentication or Authorization
- Leak HTTP details down

RFC: Should there be a AuthN/AuthZ layer here or should AuthN/AuthZ be a part of BizLog?

### Business Logic
With all the business logic inside of Plain Old Java Objects, the code is portable between frameworks and testable without a Java EE container. Data transformation should only happen when Business Logic drives the transformation and the transformation should be tested. This layer deserves very high code coverage.

Business Logic Layer should:
- Testable by plain vanilla JUnit/TestNG/whatever
- Contains all the business logic

Business Logic Layer should not:
- Transform data to enable BizLog

### Data Transformation

Data Transformation Layer should:
- Transform data to enable

Data Transformation Layer should not:

### Database Client

Database Client should:

Database Client should not:

### Database

Database should:

Database should not:
- Have any business logic unless you have performance needs and proof that the DB is more performant
