- Controller <- Receives the requests, basic validations
- Model <- Class, Entity, Structure of an Entity
- View <- Fronted, UI
- Service <- Holds the Business Logic
- Repository <- Database
- API <- Application Programming Interface

# REST API Guidelines

- Don't use verbs as API Endpoints,
	- Valid -> /video
	- Not Valid -> /upload_video
- HTTP Methods -> 
	- Get -> Fetch a Resource
	- Post -> Create a Resource
	- Put -> Update Entire Resource
	- Delete -> Delete a Resource
	- Patch -> Update part of a Resource
- https://learn.microsoft.com/en-us/azure/architecture/best-practices/api-design