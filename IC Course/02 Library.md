#### Params as a parameter
```csharp
public void usingParams(params int[] values){}
public void main(){
  usingParams(1, 2, 3, 4, 5);
}
```

#### Object Initializers
```csharp
var bob = new Person
{
  Name = "Bob",
  DOB = new DateTime(2018, 1, 1)
};
```

#### Try/Catch/Finally

