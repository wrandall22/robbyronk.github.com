# N-Tier Applications at Cru
###### Specializing in Layers, Not Applications

Our team has been talking about this and I thought it deserved some more thought and writing down.

## The Layers

From user down:
- View
- Application Logic
- data transformation
- REST Client
- REST Server
- Business Logic
- data transformation
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
### Service Layer
### REST Client
--------------
#### HTTP
--------------
### REST Server
### Business Logic
### Data Transformation
### Database Client
### Database
