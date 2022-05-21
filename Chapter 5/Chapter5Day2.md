# Chapter 5 Day 2 Quest Answers

## 1. Explain why standards can be beneficial to the Flow ecosystem.

### Standards can be beneficial to the Flow ecosystem by simplifying the process for clients of interacting with various NFT contracts. It also organizes the code for smart contract developers so that there is uniformity and standardization within the Flow ecosystem when NFT's are involved. 

## 2. What is YOUR favourite food?

### My favorite food is knowledge (deep stuff huh).

## 3. Please fix this code (Hint: There are two things wrong):

## The contract interface:

``` cadence
pub contract interface ITest {
  pub var number: Int
  
  pub fun updateNumber(newNumber: Int) {
    pre {
      newNumber >= 0: "We don't like negative numbers for some reason. We're mean."
    }
    post {
      self.number == newNumber: "Didn't update the number to be the new number."
    }
  }

  pub resource interface IStuff {
    pub var favouriteActivity: String
  }

  pub resource Stuff {
    pub var favouriteActivity: String
  }
}
```

## The implementing interface:

``` cadence
pub contract Test {
  pub var number: Int
  
  pub fun updateNumber(newNumber: Int) {
    self.number = 5
  }

  pub resource interface IStuff {
    pub var favouriteActivity: String
  }

  pub resource Stuff: IStuff {
    pub var favouriteActivity: String

    init() {
      self.favouriteActivity = "Playing League of Legends."
    }
  }

  init() {
    self.number = 0
  }
}
```
### Fix 1: On the implementing contract first line, the contract Test should implement ITest and be read as such 
``` cadence
pub contract Test: ITest {
...
}
```
### Fix 2: On the implementing contract, the resource Stuff should implement the the resource interface IStuff within the contract interface ITest by implementing as such
``` cadence
pub resource Stuff: ITest.IStuff {
...
}
```
