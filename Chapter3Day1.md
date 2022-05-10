# Chapter 3 Day 1 Quest Answers

## 1. In words, list 3 reasons why structs are different from resources.

### *Resources cannot be copied (structs can) or overwritten (structs can), and moreover resources are more secure than structs. *

## 2. Describe a situation where a resource might be better to use than a struct.

### *If you use resources for NFT's, that ensures for the owners of the NFT's that the NFT's are more secure and cannot be interfered with as easily as structs can.*

## 3. What is the keyword to make a new resource?

### *"create"*

## 4. Can a resource be created in a script or transaction (assuming there isn't a public function to create one)?

### *No a resource cannot be created a script or transacition. A resource can only be created in the contract.*

## 5. What is the type of the resource below?

```cadence
pub resource Jacob {

}
```

### "@Jacob"

## 6. Let's play the "I Spy" game from when we were kids. I Spy 4 things wrong with this code. Please fix them.

```cadence
pub contract Test {

    // Hint: There's nothing wrong here ;)
    pub resource Jacob {
        pub let rocks: Bool
        init() {
            self.rocks = true
        }
    }

    pub fun createJacob(): Jacob { // there is 1 here
        let myJacob = Jacob() // there are 2 here
        return myJacob // there is 1 here
    }
}
```

### Error 1. Should include @ sign. 
### Correction 1: pub fun createJacob(): @Jacob {

### Error 2. Cannot use "=" sign for resources
### Correction 2. let myJacob <- create Jacob()

### Error 3. Need to add "create" 
### Correction 3. let myJacob <- create Jacob()

### Error 4. Resources have to be returned by moving the resource using the "<-" to the return value.
### Correction 4. return <- myJacob
