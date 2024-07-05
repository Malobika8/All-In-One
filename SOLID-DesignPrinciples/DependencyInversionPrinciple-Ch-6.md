# Dependency Inversion Principle

```
High level modules should not directly depend on low level modules, instead they should depend on abstractions.
```

Consider a Class named *MyMessenger* thats sends message using TCPProtolHandler. TCPProtolHandler, in turn, actually sends the message.

<img width="1020" alt="Screenshot 2024-07-05 at 1 00 02 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7d52ca18-d322-48ac-b154-394d0ce28135">
<img width="865" alt="Screenshot 2024-07-05 at 12 59 41 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/45687203-fd30-4899-be23-ee4d1166f449">

We can clearly see that the High Level Module is directly dependent on Low Level Module. 

Dependency Inversion principle says that direct dependency of High Level Modules on Low Level Modules should be avoided.

### How should we avoid then?

We can have an Interface for ProtocolHandler.

<img width="811" alt="Screenshot 2024-07-05 at 1 01 18 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4adbb79c-ee24-4ddd-a8ef-bcf043f544d0">

This can be implemented by different ProtocolHandlers.

<img width="943" alt="Screenshot 2024-07-05 at 1 01 24 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bc8859ba-eada-4e49-98df-82913c67193a">

Apart from this, we can have a *ProtocolHandlerFactory* that can get us an instance of any requested ProtolHandler.

<img width="985" alt="Screenshot 2024-07-05 at 1 04 13 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b86e181b-3c6e-41bf-8acd-6327190999e2">

Now, *MyMessenger* isn't dependent on any particular Protol Handler. It is rather dependent on Interface *ProtocolHandler* which
is an abstraction.

<img width="968" alt="Screenshot 2024-07-05 at 1 05 00 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d0cd7517-b23b-4c56-aa85-2ed32b46739b">


#### High level module isn't dependent on low level module. It is rather dependent on abstraction. This is what *Dependency Inversion Principle* intends.
