# Chapter 4 Day 1 Quest Answers

## 1. Explain what lives inside of an account.

### Inside an account lives contract code and account storage. The account storage is where all the data in the account is stored. The contract code is where all the contracts that got deployed to the account live.

## 2. What is the difference between the /storage/, /public/, and /private/ paths?

### In the account storage there are three different paths to obtain data - the /storage/, /public/, and /private/ paths. The /storage/ path is where all the data of the account lives, and only the owner of the account can access this path. The /public/ path is where all the data that the account owners wants to be public information lives, so anybody can access the data. The /private/ path is where all the data that the account owner wants to be private lives. The /private/ path can only be accessed by the account owners and also whoever the account owner wants to give access to.

## 3. What does .save() do? What does .load() do? What does .borrow() do?

### The .save() function is a function that stores data into your account. It takes in two parameters - the data to be saved in the account and the /storage/ path where the data will be stored. 

### The .load() function is a function that takes data out of the account storage. It takes in one parameter - the /storage/ path where the data should be pulled from. Moreover, when the .load() function is used, it is important to note that it returns as an optional.

### The .borrow() function is a function that takes a peek into the account using a reference to the data (most likely a resource) in the storage. It takes in one parameter - the /storage/ path where the reference to the resource should be pulled from. The .borrow() function allows for the resource to be looked at without having to move it from the account storage.

## 4. Explain why we couldn't save something to our account storage inside of a script.

### Data cannot be altered using scripts. Instead, to alter data a transaction has to be used. Since saving something to the account storage would require the data to be altered on the blockchain, a script cannot be used.
### Moreover, you can only access the account storage in the prepare phase of a transaction.

## 5. Explain why I couldn't save something to your account.

### My account storage is only accesible the account owner (me) using a "AuthAccount" when the owner (oh yes, me again) confirms a transaction. So people cannot save things in my account without using my AuthAccount. The only thing you can do is see things in my account storage that are public.

## 6. Define a contract that returns a resource that has at least 1 field in it. Then, write 2 transactions:

``` cadence
pub contract Chp4Day1 {

  pub resource Insult {
    pub let insult: String

    init() {
      self.insult = "Dwight- You're a kissass."
    }
  }

  pub fun createInsult(): @Insult {
    return <- create Insult()
  }

  init() {
    
  }
}
```

## 6i. A transaction that first saves the resource to account storage, then loads it out of account storage, logs a field inside the resource, and destroys it.

``` cadence
import Chp4Day1 from 0x01

transaction() {
  prepare(signer: AuthAccount) {
    let supaHotFiyaResource <- Chp4Day1.createInsult()
    signer.save(<- supaHotFiyaResource, to: /storage/SupaHotFiyaResource) 
    
    let supaHotFiyaResource2 <- signer.load<@Chp4Day1.Insult>(from: /storage/SupaHotFiyaResource)
                                ?? panic("`@Chp4Day1.Insult` a'int here my dude.")
    log(supaHotFiyaResource2.insult) 
    
    destroy supaHotFiyaResource2
  }

  execute {

  }
}
```
<img width="403" alt="Screen Shot 2022-05-18 at 2 39 02 PM" src="https://user-images.githubusercontent.com/104539205/169142306-1bc0ea6f-a8b5-4fc2-89bb-0f680e687d0a.png">

## 6ii. A transaction that first saves the resource to account storage, then borrows a reference to it, and logs a field inside the resource.

``` cadence
import Chp4Day1 from 0x01
transaction() {
  prepare(signer: AuthAccount) {
    let supaHotFiyaResource <- Chp4Day1.createInsult()
    signer.save(<- supaHotFiyaResource, to: /storage/SupaHotFiyaResource) 
    
    let supaHotFiyaResource2 = signer.borrow<&Chp4Day1.Insult>(from: /storage/SupaHotFiyaResource)
                                ?? panic("`@Chp4Day1.Insult` a'int here my dude.")
                                
    log(supaHotFiyaResource2.insult) 
  }

  execute {

  }
}
```
<img width="435" alt="Screen Shot 2022-05-18 at 2 45 29 PM" src="https://user-images.githubusercontent.com/104539205/169143317-b203d57d-4329-4446-b4b6-b7884b0a2009.png">
