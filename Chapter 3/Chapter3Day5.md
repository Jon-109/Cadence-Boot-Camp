# Chapter 3 Day 5 Quest Answers

## For today's quest, you will be looking at a contract and a script. You will be looking at 4 variables (a, b, c, d) and 3 functions (publicFunc, contractFunc, privateFunc) defined in SomeContract. In each AREA (1, 2, 3, and 4), I want you to do the following: for each variable (a, b, c, and d), tell me in which areas they can be read (read scope) and which areas they can be modified (write scope). For each function (publicFunc, contractFunc, and privateFunc), simply tell me where they can be called.
``` cadence
access(all) contract SomeContract {
    pub var testStruct: SomeStruct

    pub struct SomeStruct {

        //
        // 4 Variables
        //

        pub(set) var a: String

        pub var b: String

        access(contract) var c: String

        access(self) var d: String

        //
        // 3 Functions
        //

        pub fun publicFunc() {}
        //Function Access Scope - All (Can be called anywhere)
        
        access(contract) fun contractFunc() {}
        //Function Access Scope - Current, Inner & Containing Contract 
        // can be called on functions #1 (structFunc()), #2 (resourceFunc()), & #3 (questsAreFun)

        access(self) fun privateFunc() {}
        //Function Access Scope - Current & Inner
        // can only be called on function #1 (structFunc())


        pub fun structFunc() {
             
             //Variable A
             //Read Scope - All
             //Write Scope - All
             
             //Variable B
             //Read Scope - All
             //Write Scope - All
             
             //Variable C
             //Read Scope - All
             //Write Scope - All
             
             //Variable D
             //Read Scope - All
             //Write Scope - All
        }

        init() {
            self.a = "a"
            self.b = "b"
            self.c = "c"
            self.d = "d"
        }
    }

    pub resource SomeResource {
        pub var e: Int

        pub fun resourceFunc() {
             //Variable A
             //Read Scope - All
             //Write Scope - All
             
             //Variable B
             //Read Scope - All
             //Write Scope - Not writable
             
             //Variable C
             //Read Scope - All
             //Write Scope - Not writable
             
             //Variable D
             //Read Scope - Not Readable (private)
             //Write Scope - Not writable
        }

        init() {
            self.e = 17
        }
    }

    pub fun createSomeResource(): @SomeResource {
        return <- create SomeResource()
    }

    pub fun questsAreFun() {
             //Variable A
             //Read Scope - All
             //Write Scope - All
             
             //Variable B
             //Read Scope - All
             //Write Scope - Not writable
             
             //Variable C
             //Read Scope - All
             //Write Scope - Not writable
             
             //Variable D
             //Read Scope - Not Readable (private)
             //Write Scope - Not writable
    }

    init() {
        self.testStruct = SomeStruct()
    }
}
```
This is a script that imports the contract above:
``` cadence
import SomeContract from 0x01

pub fun main() {
             //Variable A
             //Read Scope - All
             //Write Scope - Not writable (since it is within a script)
             
             //Variable B
             //Read Scope - All
             //Write Scope - Not writable
             
             //Variable C
             //Read Scope - Not Readable (private)
             //Write Scope - Not writable
             
             //Variable D
             //Read Scope - Not Readable (private)
             //Write Scope - Not writable
}
```


  
