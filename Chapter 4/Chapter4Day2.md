# Chapter 4 Day 2 Quest Answers

## What does .link() do?

### The .link() function is a function that assigns references of resources to either the /public/ path or /private/ path of the account storage. The .link() function does not store data in the /public/ path or /private/ path, but instead gives the /public/ path or /private/ path the capability to see references of data that is "linked" such as resources in the /storage/ path.

## 2. In your own words (no code), explain how we can use resource interfaces to only expose certain things to the /public/ path.

### Resource interfaces restrict people from accessing data we do not want them to have access to. The resource interface acts as a filter to restrict the fields that are publicly accessible. When the resources are linked to the /public/ path using the .link() function, to restrict access to specific data the developer should link the reference to the resource with a implemented resource interface as well.

## 3. Deploy a contract that contains a resource that implements a resource interface. Then, do the following:

``` cadence
pub contract Chp4Day2 {

  pub resource interface IInsult {
    pub var insult: String
  }

  pub resource Insult: IInsult {
    pub var insult: String
    pub var scarn: String

    init() {
      self.insult = "Angela - Where are you? I couldn't see you from behind that grain of rice."
      self.scarn = "Michael Scott"
    }
  }

  pub fun createInsult(): @Insult {
    return <- create Insult()
  }
}
```

## 3i. In a transaction, save the resource to storage and link it to the public with the restrictive interface.

``` cadence 
import Chp4Day2 from 0x01

transaction() {
  prepare(signer: AuthAccount) {
    let supaHotFiyaResource <- Chp4Day2.createInsult()
    
    signer.save(<- supaHotFiyaResource, to: /storage/SupaHotFiyaResource) 
  
    signer.link<&Chp4Day2.Insult{Chp4Day2.IInsult}>(/public/SupaHotFiyaResource, target: /storage/SupaHotFiyaResource)
  }

  execute {

  }
}
```

## 3ii. Run a script that tries to access a non-exposed field in the resource interface, and see the error pop up.

```cadence
import Chp4Day2 from 0x01

pub fun main(address: Address): String {
  let publicCapability: Capability<&Chp4Day2.Insult{Chp4Day2.IInsult}> = getAccount(address).getCapability<&Chp4Day2.Insult{Chp4Day2.IInsult}>(/public/SupaHotFiyaResource)

  let dundie: &Chp4Day2.Insult{Chp4Day2.IInsult} = publicCapability.borrow() ?? panic("Not today satan. You'll never know who the Scarn truly is.")

  return dundie.scarn
  //not accessible.. the identity of the scarn is top secret
}
```
<img width="326" alt="Screen Shot 2022-05-19 at 2 24 13 PM" src="https://user-images.githubusercontent.com/104539205/169386461-3ba1a83a-8d89-4163-af3c-cafa2213a328.png">


## 3iii. Run the script and access something you CAN read from. Return it from the script.
``` cadence
import Chp4Day2 from 0x01

pub fun main(address: Address): String {
  let publicCapability: Capability<&Chp4Day2.Insult{Chp4Day2.IInsult}> = getAccount(address).getCapability<&Chp4Day2.Insult{Chp4Day2.IInsult}>(/public/SupaHotFiyaResource)

  let dundie: &Chp4Day2.Insult{Chp4Day2.IInsult} = publicCapability.borrow() ?? panic("Not today satan. Capability is not here.")

  return dundie.insult
  //okay fine you can know this 
}
```
<img width="720" alt="Screen Shot 2022-05-19 at 2 22 51 PM" src="https://user-images.githubusercontent.com/104539205/169386253-80f53f45-745a-424d-b061-5a96c2e25404.png">

