# Chapter 5 Day 1 Quests Answers

## 1. Describe what an event is, and why it might be useful to a client.

### An event is a way for the contract to easily communicate that something has occurred. They are useful because the alternative would be to constantly check the state of things in the contract to see if anything changed, and this isn't nearly as efficient having the contract broadcast when events occur.

## 2. Deploy a contract with an event in it, and emit the event somewhere else in the contract indicating that it happened.

``` cadence
pub contract Chp5Day1 {

  pub event NFTCreated(id: UInt64)

  pub resource Insult {

    pub let id: UInt64

    init() {
      self.id = self.uuid
    }
  }

  pub fun createInsult(): @Insult {
    let insult <- create Insult()
    emit NFTCreated(id: insult.id)
    return <- insult
  }
}
```

## 3. Using the contract in step 2), add some pre conditions and post conditions to your contract to get used to writing them out.
``` cadence
pub contract Chp5Day1 {

  pub event NFTCreated(id: UInt64)

  pub resource Insult {

    pub let id: UInt64
    pub var roast: UInt64

    //creating this function to multiply the roast variable by two and the variable must be greater than zero
    //the pre conditions will confirm the roast variable is greater than 0
    //the post conditions will check that the value will have have new roast mod before roast = 0
    pub fun multiplyByTwo() {
      
    pre {
      self.roast > 0: "Not greater than zero" 
    }
    post {
      self.roast % before(self.roast) == 0: "Something is off."
    }

      self.roast = self.roast * 2
    }

    init() {
      self.id = self.uuid
      self.roast = 3
    }
  }

  pub fun createInsult(): @Insult {
    let insult <- create Insult()
    emit NFTCreated(id: insult.id)
    return <- insult
  }
}
```

## 4. For each of the functions below (numberOne, numberTwo, numberThree), follow the instructions.

``` cadence
pub contract Test {

  // TODO
  // Tell me whether or not this function will log the name.
  // name: 'Jacob'
  pub fun numberOne(name: String) {
    pre {
      name.length == 5: "This name is not cool enough."
    }
    log(name)
  }

  // TODO
  // Tell me whether or not this function will return a value.
  // name: 'Jacob'
  pub fun numberTwo(name: String): String {
    pre {
      name.length >= 0: "You must input a valid name."
    }
    post {
      result == "Jacob Tucker"
    }
    return name.concat(" Tucker")
  }

  pub resource TestResource {
    pub var number: Int

    // TODO
    // Tell me whether or not this function will log the updated number.
    // Also, tell me the value of `self.number` after it's run.
    pub fun numberThree(): Int {
      post {
        before(self.number) == result + 1
      }
      self.number = self.number + 1
      return self.number
    }

    init() {
      self.number = 0
    }

  }

}
```
### Function numberOne - The function will log "Jacob" since it meets the precondition that the length of name was 5 characters.
### Function numberTwo - The function will return the value "Jacob Tucker" since it meets the postcondition that the value of name be exactly "Jacob Tucker" since " Tucker" was concatenated to the value "Jacob"
### Function numberThree - The function will not log the updated number since it does meets the postcondition that the number before the function is equivalent to the number plus 1 after the function, which it is not. In this function without postconditions, the number value is initially 0 but then after the function it comes 1. So it adds one to the number variable. The post conditions would only be true if the post conditions compared the initial value with the post value subtracted by one instead of adding one to the post value as such:
``` cadence
post {
        before(self.number) == result - 1
      }
```
