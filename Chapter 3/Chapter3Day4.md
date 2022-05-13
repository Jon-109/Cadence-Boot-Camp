# Chapter 3 Day 4 Quest Answers

## 1. Explain, in your own words, the 2 things resource interfaces can be used for (we went over both in today's content)

### One thing resource interfaces can be used for is it lays out requirements for a resource or struct to implement. When a resource interface is implemented by a resource, the interface must define all the variables and functions that the resource has as well. Another thing resource interfaces can be used for is it allows for developers to limit the resources to only use what the interface exposes.

## 2. Define your own contract. Make your own resource interface and a resource that implements the interface. Create 2 functions. In the 1st function, show an example of not restricting the type of the resource and accessing its content. In the 2nd function, show an example of restricting the type of the resource and NOT being able to access its content.

``` cadence
pub contract Chp3Day4 {

    pub resource interface IRobot {
      pub var idNum: Int
    }

    pub resource Robot: IRobot {
      pub var idNum: Int
      pub var humanName: String

      pub fun updateName(newName: String): String {
        self.humanName = newName
        return self.humanName // returns the new name
      }

      init() {
        self.idNum = 109
        self.humanName = "Mark Zuckerberg"
      }
    }

    pub fun noRestrictions() {
      let Zuckerberg: @Robot <- create Robot()
      Zuckerberg.updateName(newName: "Markie Poo")
      log(Zuckerberg.humanName) // this should print "Markie Poo" since the resource does not implement the resource interface IRobot

      destroy Zuckerberg
    }

    pub fun yesRestrictions() {
      let Markie: @Robot{IRobot} <- create Robot()
      let newName = Markie.updateName(newName: "Markie Poo") // this does not work since the resource interface does not define the variable humanName with object type String
      log(newName)

      destroy Markie
    }
}
```

## 3. How would we fix this code?

``` cadence
pub contract Stuff {

    pub struct interface ITest {
      pub var greeting: String
      pub var favouriteFruit: String
    }

    // ERROR:
    // `structure Stuff.Test does not conform 
    // to structure interface Stuff.ITest`
    pub struct Test: ITest {
      pub var greeting: String

      pub fun changeGreeting(newGreeting: String): String {
        self.greeting = newGreeting
        return self.greeting // returns the new greeting
      }

      init() {
        self.greeting = "Hello!"
      }
    }

    pub fun fixThis() {
      let test: Test{ITest} = Test()
      let newGreeting = test.changeGreeting(newGreeting: "Bonjour!") // ERROR HERE: `member of restricted type is not accessible: changeGreeting`
      log(newGreeting)
    }
}
```

### To fix this code I would change it to the following
``` cadence 
pub contract Stuff {

    pub struct interface ITest {
      pub var greeting: String
      pub var favouriteFruit: String
      pub fun changeGreeting(newGreeting: String): String
    }

    pub struct Test: ITest {
      pub var greeting: String
      pub var favouriteFruit: String

      pub fun changeGreeting(newGreeting: String): String {
        self.greeting = newGreeting
        return self.greeting // returns the new greeting
      }

      init() {
        self.greeting = "Hello!"
        self.favouriteFruit = "Apple"
      }
    }

    pub fun fixThis() {
      let test: Test{ITest} = Test()
      let newGreeting = test.changeGreeting(newGreeting: "Bonjour!")
      log(newGreeting)// "Bonjour!"
    }
}
```
<img width="570" alt="Screen Shot 2022-05-12 at 10 38 32 PM" src="https://user-images.githubusercontent.com/104539205/168206574-b39f301d-1f94-467f-835c-55a5f75329a4.png">
