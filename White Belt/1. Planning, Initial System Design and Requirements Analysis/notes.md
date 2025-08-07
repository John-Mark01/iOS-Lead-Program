# Are ```Singletons``` and ```Global Systems``` damaging your system design?

## How can i test the ```network layer```?
- there is nothing wrong with the network being a singleton and still be testable



## Should I be using ```Singletons```?
- definition: the ```singleton``` pattern is a way to make sure a class has only one instance. The class itself is responsible for it's own instance. The ```singleton``` has only ONE access point. Nobody else should be able to make new instances of a class.

### Singleton Types:
#### 1. Singleton with capital 'C'
```
class Singleton {
    static let shared = Singleton()
    
    private init() {}
}
```
- it's initializer is private, so no one except itself can reinstantiate the instance.
- it only has one access point - ```Singleton.shared```
- ```shared``` is static

#### 2. Singleton with lowercase 'c'
```
class Singleton {
    static let shared = Singleton()
    
}
```
- the difference is that now the initializer is accessed outside the ```Singleton``` class. This means that you can use ```Singleton.shared```, or create a new instance ```let singleton = Singleton(data: Data)```, and probably add a configuraion.
However the class instatiates itself with the default configuration, and still follows the singleton pattern.
- the main focus is that ```shared``` is a ```let```, which means it only has a getter.
- this type ```Singleton with a lowercase 'c'``` is found in Swift API's like: ```URLSession.shared```, so you can do this:
```
//access shared instance

func downloadData() async {
    let url = URL(string: "https://example.com/some/data")!
    try? await URLSession.shared.download(from: url)
}
```
or,
```
//create a new instance of URLSession

func downloadData() async {
    let url = URL(string: "https://example.com/some/data")!
    let session = URLSession(configuration: .ephemeral)
    try? await session.download(from: url)
}
```


#### 3. A misunderstood concept of a Singleton - global state object
```
class Singleton {
    // shared instance has a getter and a setter - NOT thread safe
    // ❌ Bad implementation for Networking
    static var shared = Singleton()
}
```

- This means that any client in the app can rewrite the ```shared``` property (the instance) of the class —— ```Singleton.shared = Singleton()```. THis is very bad, since now this is ```NOT``` thread safe because two objects can try to access or change the class at the same time, resulting in ```Unsafe mutable state```... and a runtime error.
- This is no longer a ```Singleton``` or a ```singleton```, this is a global state object.

  
### Conclusion
- In most cases the Singleton pattern is used for API clients. Then theese clients are accessed through ViewModels and ViewCntrollers. This way is not testable, and does not give freedom to the ViewModel or Controller.

```1. First Step``` is to inject the API client, and extend implementation of the Singleton class for every Moduli
   - the ViewController is making a ```property injection``` of the client, so that it can be replaced with a mock client.

```2. Second Step``` is to invert the dependency - DIP (SOLID)
  - the API Client(the singleton) now depends on the modules through ```Abstraction``` - ```closure, or protocol```.
  This way the module does not need or does not care about the API Client. It only says: 'I need this and this logic'
