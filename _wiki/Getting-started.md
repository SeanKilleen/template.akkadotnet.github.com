####How to write your first actor:
```csharp
//Create an (immutable) message type that your actor will respond to
public class Greet
{
    public Greet(string who)
    {
        Who = who;
    }
    public string Who { get;private set; }
}

//Create the actor class
public class GreetingActor : ReceiveActor
{
    public GreetingActor()
    {
        Receive<Greet>(greet => Console.WriteLine("Hello {0}", greet.Who));
    }
}
```
####Usage:
```csharp
//create a new actor system (a container for your actors)
var system = ActorSystem.Create("MySystem");
//create your actor and get a reference to it.
//this will be an "ActorRef", which is not a reference to the actual actor instance
//but rather a client or proxy to it
var greeter = system.ActorOf<GreetingActor>("greeter");
//send a message to the actor
greeter.Tell(new Greet("Roger"));
