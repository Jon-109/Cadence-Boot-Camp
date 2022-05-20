# Chapter 4 Day 3 Quest Answers

## 1. Why did we add a Collection to this contract? List the two main reasons.

### When NFT's are created they need a unique storage path and it is much easier to organize all the resources in a collection created by the contract at one storage path rather than individual storage paths for each NFT. Moreover since only the account owner has access to the storage path, the owner cannot receive NFT's from other people. A collection fixes this.

## 2. What do you have to do if you have resources "nested" inside of another resource? ("Nested resources")

### If you have resources (perhaps NFT's) "nested" inside of another resource (perhaps a collection) in Cadence, you must declare a destroy function that manually destroys those "nested" resources (perhaps NFTs) with the destroy keyword.

## 3. Brainstorm some extra things we may want to add to this contract. Think about what might be problematic with this contract and how we could fix it.

Idea #1: Do we really want everyone to be able to mint an NFT? 🤔.

Idea #2: If we want to read information about our NFTs inside our Collection, right now we have to take it out of the Collection to do so. Is this good?

### Fix 1: Assign an account to be owner of a resource that gives permission to be the minter of the NFT's. Place the function to mint NFT's in that minter resource just assigned to the account.  

### Fix 2: Link the resources in the collection to the public path of the account storage so that they can have the capability to view the reference of the resource without having to move the resource itself.

### Fix 3: Make the collection resource implement a resource interface to restrict access to the withdraw function to eliminate the public from being able to withdraw from the collection. The resource interface will expose only what we want so we can restrict access to other things in the collection as well.

