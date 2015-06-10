# Routific npm module

This node library is a client to interact with the [Routific API](http://docs.routific.com/v1.0/docs/api-reference)

# Usage

Install the npm module:

```
npm install routific
```

A simple login example:

```
Routific = require('routific');

client = new Routific.Client();

client.login("test@test.com", "123456", function(err, response){
    // ...
});
```


# Initialization

The Routific `Client` constructor accepts an optional configuration object as a first argument.

```
client = new Routific.Client(options);
```

Valid options:
- `url`: Routific API url. This is for internal use only. Default `"https://api.routific.com"`.
- `version`: Version of the API to use. Default `1`.
- `token`: User token to use for authenticated operations. This is optional, performing a login will set it too. Default `null`.


# Operations

## Login

It calls the Login endpoint and keeps the received token for the following authenticated calls.

```
client.login(email, password, function(error, response){
    //...
})
```

## VRP route

It calls the VRP endpoint (long version) and waits until the job is processed. It returns the job output, as it would do callinf the short VRP endpoint.

```
vrp = new Routific.Vrp();
vrp.addVisit(visitID1, {
    location: {
        name: "Visit1 name",
        lat: 49.227607,
        -123.1363085
    },
    start: "8:00",
    end: "16:00",
    duration: 10
});
vrp.addVehicle(vehicleID1, {
    start_location:{
        id: "depot",
        lat: 49.2553636,
        lng: -123.0873365
    },
    end_location:{
        id: "depot",
        lat: 49.2553636,
        lng: -123.0873365
    }
});
client.route(vrp, function(err, solution){
    //...
})
```
