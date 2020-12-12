# JAVASCRIPT-PROMISES-AND-ASYNC-AWAIT
Basic usage of promises and async and await

## Contains
- Asynchronous programming
- Consuming & Creating Promises
- Using async & await in JavaScript


## Understanding Promises
Promises make things better but not necessarily simple.Let see fairly common problem of fetching data and how asyncronous creates a bug. The bug here is that when we call this function raceCondition it should first execute the **xhr** request and then **xhr2** ideally but instead the **orders/1** execute first and then **orderStatus** 

```
export function raceCondition() {
  let xhr = new XMLHttpRequest(); // creates new XML http request against the api
  let statuses = [];
  xhr.open("GET","http://localhost:3000/orderStatuses"); // specifies the path and type of request
  xhr.onload = () => { // it is kind of function that can be taught as success
    statuses = JSON.parse(xhr.responseText);
  };
  xhr.send(); // this is used to fire the request
  
  let xhr2 = new XMLHttpRequest();
  xhr2.open("GET","http://localhost:3000/orders/1");
  xhr2.onload = () => {
    const order = JSON.parse(xhr2.responseText);
    const description = statuses.map(t =>{
      if(t.id === order.orderStatusId) {
        return t.description;
      }
    })[0];
    setText(`Order Status: ${description}`);
  };
  xhr2.send();  
  
}
```
