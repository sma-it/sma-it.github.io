---
title: Overerving
---

```csharp
class Animal {
  public int legs { get; set; }
  public bool canFly { get; set; }
  public float lifeExpectancy { get; set; }
  
  public override string ToString() {
    return "this animal has " + legs + " legs and "
       + canFly ? " can " : " cannot "
       + " fly.";
  }
  
  public abstract string Talk();
}
```
```csharp
class Mammal : Animal {
  public Mamal(int lifeExpectancy) {
    legs = 4;
    canFly = false;
    this.lifeExpectancy = lifeExpectancy;
  }
  
  public string Talk() {
    return "growl";
  }
}

class Bird : Animal {
  public Bird(int lifeExpectancy) {
    legs = 2;
    canFly = true;
    this.lifeExpectancy = lifeExpectancy;
  }
  
  public void SelfDestruct() {
    legs = 0;
    canFly = false;
    lifeExpectancy = 0;
  }
  
  public override string ToString() {
    return "this animal has " + legs + " legs and "
        + canFly ? " can " : " cannot "
        + " fly.";
    }
  }
  
  public string Talk() {
    return "squeak!";
  }
}
```


