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
- Extensively transform data
- Format data
- Use $http or $resource
- Have any notion of what HTTP is

### Service Layer

Service Layer should:

Service Layer should not:


### REST Client

REST Client should:

REST Client should not:

--------------
#### :arrow_up: Client Side/Front End
#### :arrow_up_down: HTTP
#### :arrow_down: Server Side/Back End
--------------

### REST Server

REST Server should:

REST Server should not:

### Business Logic

Business Logic Layer should:

Business Logic Layer should not:

### Data Transformation

Data Transformation Layer should:

Data Transformation Layer should not:

### Database Client

Database Client should:

Database Client should not:

### Database

Database should:

Database should not:
