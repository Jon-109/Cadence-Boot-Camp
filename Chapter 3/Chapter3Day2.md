# Chapter 3 Day 2 Quest Answers

## 1. Write your own smart contract that contains two state variables: an array of resources, and a dictionary of resources. Add functions to remove and add to each of them. They must be different from the examples above.

``` cadence
pub contract Emerald {

    pub var arrayOfInsults: @[Insult]
    pub var dictionaryOfInsults: @{String: Insult}

    pub resource Insult {
        pub let getRoasted: String
        
        init() {
            self.getRoasted = "Pam - You failed art school. Boom Roasted."
        }
    }

    pub fun addInsultToDictionary(insult: @Insult) {
        let key = insult.getRoasted
        
        let oldInsult <- self.dictionaryOfInsults[key] <- insult
        destroy oldInsult
    }

    pub fun removeInsultFromDictionary(key: String): @Insult {
        let insult <- self.dictionaryOfInsults.remove(key: key) ?? panic("There ain't no damn insults..")
        return <- insult
    }

    pub fun addGreetingToArray(insult: @Insult) {
        self.arrayOfInsults.append(<- insult)
    }

    pub fun removeGreetingFromArray(index: Int): @Insult {
        return <- self.arrayOfInsults.remove(at: index)
    }

    init() {
        self.arrayOfInsults <- []
        self.dictionaryOfInsults <- {}

    }

}

```
