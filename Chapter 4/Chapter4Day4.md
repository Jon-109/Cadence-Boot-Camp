# Chapter 4 Day 4 Quest Answers

## 1. Take our NFT contract so far and add comments to every single resource or function explaining what it's doing in your own words. Something like this:

``` cadence
pub contract CryptoPoops {
  pub var totalSupply: UInt64
  
  pub resource NFT {  // This is an NFT resource that contains an id, name, favouriteFood, and luckyNumber
    pub let id: UInt64 //this variable represents the id of each NFT 

    pub let name: String //name field of the NFT
    pub let favouriteFood: String //favorite food field of the NFT
    pub let luckyNumber: Int //lucky number field of the NFT

    init(_name: String, _favouriteFood: String, _luckyNumber: Int) {
      self.id = self.uuid //initializes the id variable to the unique resource id that Flow assigns it

      self.name = _name //initializes to String value is for the _name variable
      self.favouriteFood = _favouriteFood //initializes to String value is for the _favouriteFood variable
      self.luckyNumber = _luckyNumber //initializes to Int value is for the _luckyNumber variable
    }
  }

  // Below a resource interface that allows us to expose only what we want to the public
  // the deposit function, getID function, and the borrow function are all avaiable to the public since they are implemented to the resource Collection
  pub resource interface CollectionPublic {
    pub fun deposit(token: @NFT) 
    pub fun getIDs(): [UInt64]
    pub fun borrowNFT(id: UInt64): &NFT
  }

  // below is a resource Collection that implements the resource interface CollectionPublic
  //this resource allows us to group the NFT's created by this contract into a singular storage path to make it easily accessible
  pub resource Collection: CollectionPublic {
    pub var ownedNFTs: @{UInt64: NFT}   //this variable contains a dictionary of resources (NFTs) along with a unique id for each one

    pub fun deposit(token: @NFT) { //this function takes in a token id and deposits the resource (@NFT) into the collection, which is a dictionary
      self.ownedNFTs[token.id] <-! token 
    }

    pub fun withdraw(withdrawID: UInt64): @NFT { //this function takes in a id number and withdraws the correlated resource NFT out the collection if it exists
      let nft <- self.ownedNFTs.remove(key: withdrawID) 
              ?? panic("This NFT does not exist in this Collection.") // if the collection does not exist, then the program will abort and print out what is specified
      return <- nft //this function returns a resource nft
    }

    pub fun getIDs(): [UInt64] { //this function gets the ID's of all the NFT's in the collection
      return self.ownedNFTs.keys
    }

    pub fun borrowNFT(id: UInt64): &NFT { //this function takes in an id number as a parameter and borrows a reference of the resource matched with the inputted id number in the collection and returns the public information 
      return &self.ownedNFTs[id] as &NFT
    }

    init() { //this initializes the ownedNFTs into an empty dictionary
      self.ownedNFTs <- {}
    }

    destroy() { //this is a function that if called will destroy all the resources in the collection
      destroy self.ownedNFTs
    }
  }

  pub fun createEmptyCollection(): @Collection { //this function saves the collection to account storage and returns an empty collection
    return <- create Collection() //it returns a new empty resource collection
  }

  pub resource Minter { //this resource is allocated to the desired account to grant capabilities to mint the NFTs

    pub fun createNFT(name: String, favouriteFood: String, luckyNumber: Int): @NFT { //this function creates an NFT with a name, favorite food, and lucky number parameters
      return <- create NFT(_name: name, _favouriteFood: favouriteFood, _luckyNumber: luckyNumber) //returns a newly created nft with the inputted parameters
    }

    pub fun createMinter(): @Minter { //this function creates the resource Minter 
      return <- create Minter() //returns a newly created resource Minter
    }

  }

  init() {
    self.totalSupply = 0 //the total supply of the NFT's is initialized at ZERO until one is created
    self.account.save(<- create Minter(), to: /storage/Minter) //this creates the resource Minter and saves it into the account storage of the account who deployed the contract
  }
}
```

