# Chapter 3 Day 3 Quest Answers

## 1. Define your own contract that stores a dictionary of resources. Add a function to get a reference to one of the resources in the dictionary.

``` cadence
pub contract Chp3Day3 {

    pub var dictionaryOfSongs: @{String: Song}

    pub resource Song {
        pub let lyric: String
        init(_lyric: String) {
            self.lyric = _lyric
        }
    }

    pub fun getReference(key: String): &Song {
        return &self.dictionaryOfSongs[key] as &Song
    }

    init() {
        self.dictionaryOfSongs <- {
            "U Can't Touch This": <- create Song(_lyric: "Stop.. Hammertime"), 
            "Low": <- create Song(_lyric: "Boots With The Fur")
        }
    }
}
```

## 2. Create a script that reads information from that resource using the reference from the function you defined in part 1.

``` cadence 
import Chp3Day3 from 0x01

pub fun main(): String {
  let ref = Chp3Day3.getReference(key: "U Can't Touch This")
  return ref.lyric 
}
```
<img width="493" alt="Screen Shot 2022-05-11 at 2 30 39 PM" src="https://user-images.githubusercontent.com/104539205/167930648-b4c48414-80b7-4ddf-ba4a-5ee262db0a22.png">



## 3. Explain, in your own words, why references can be useful in Cadence.

### Resources are diffucult to move around given their strict security in Cadence, so to be able to indirectly see or alter the data in the resource without having to move it anywhere is beneficial to developers. 
