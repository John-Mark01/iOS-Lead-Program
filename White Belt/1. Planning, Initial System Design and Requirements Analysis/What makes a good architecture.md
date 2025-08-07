# What makes a good architecture?

- a architecture is the ```structure``` of a software.
- a good architecture can make a software 'soft', or in other words ```flexible```, ```scalable``` or ```reusable```.

## Bad Architecture ❌
- no requirements, just a saying, like: 'I need a social media app...' (this leaves a developer guesing what actually needs to be built)
- a lot of assumptions
- no ```use cases```/```edge cases``` - if this fails, then this needs to happen, etc...

## Good architecture ✅
- a good ```BDD```/```User Story``` (Behavioural Driven Development). The client should explain without technicality what his software needs to do.
  For example:
    1. I open the app
    2. The social app refreshes and pull new feed into my app
    3. I want the feed to be images with a title.
    4. When i close the app I want to send a message that I have been logged in.
  This is also known as the app's ```Requirements```.

- after we get our ```User Story```, then we can move on to the ```Use Cases```. 
This is the part where we are more technical and procedural. We add more clarity for how the ```User Story``` will look like in code.
  For example:
    1. User opens the app
    2. The app makes a request to API
    3. ```IF``` the user has internet connectivity, ```THEN``` download data.
    4. ```IF``` the user is offline, download saved cache.

  This gives the developer more clarity.
  Okay. We need a API, we need a Caching system, we need a app state. We need a Data module, and so on...

## Why do we need diagrams?
- it is a sort of communication
- it is a message for us in the future
- it's clarity, and a validator.
