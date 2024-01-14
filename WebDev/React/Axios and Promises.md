Axios is a Promise based HTTP client for the browser and node.js.

The documentation from Mozilla states the following about promises:
> A Promise is an object representing the eventual completion or failure of an asynchronous operation.

A promise can have three distinct states:
1. Pending: it means that the final value (one of the following two) is note available yet.
2. Fulfilled/resolved: it means that the operation has been completed and the final value is available, which generally is a successful operation. 
3. Rejected: it means that an error prevented the final value from being determined, which generally represents a failed operation.

Since we are interacting with external systems when using Axios, it makes sense to use [[useEffect]] hooks.
## Axios Methods
#### then
The 'then' method is incredibly important in Axios, as it instructs what to do after the http request has been completed. Most commonly, it is used to access the result (data mostly) of the operation represent by the promise.
#### Get
The command `axios.get` initiates the fetching of data, generally from a server, as well as registers the function following .then as an [[event handler]] for the operation.

Let's take a look at an example of an effect hook being used with axios:
![[Pasted image 20240109095912.png]]


#### Post
A basic axios POST request, written in a function within React looks like:
![[Pasted image 20240109142849.png]]
- A POST request takes two parameter
	- The address of the location to which in the information is being posted.
	- The information being posted. In this case an object named noteObject.


#### Put
#### Patch
