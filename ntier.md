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
Interface: provide promises to the Application Logic layer, consume promises from the REST Client and other services

Service Layer should:
- Contain any extensive Client Side transformations or aggregations of data
- DRY up the applog layer

Service Layer should not:
- Use $http or $resource


### REST Client
Interface: provide promises to the service layer, HTTP to the server.

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

REST Server should:
- Abstract away HTTP details

REST Server should not:

### Business Logic

Business Logic Layer should:
- Testable by plain vanilla JUnit/TestNG/whatever

Business Logic Layer should not:
- 

### Data Transformation

Data Transformation Layer should:

Data Transformation Layer should not:

### Database Client

Database Client should:

Database Client should not:

### Database

Database should:

Database should not:
