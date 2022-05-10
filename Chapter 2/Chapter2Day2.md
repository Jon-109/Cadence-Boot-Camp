# Chapter 2 Day 2 Quests
## 1. Explain why we wouldn't call changeGreeting in a script.

*A script is only used to view data, so we have to call changeGreeting in a transaction instead because transactions allow for the data to be modified.* 

## 2. What does the AuthAccount mean in the prepare phase of the transaction?

*AuthAccount acts as a confirmation for the user in prepare phase of the transaction. The confirmation ensures the user approves of the transaction and wants to continue.*

## 3. What is the difference between the prepare phase and the execute phase in the transaction?

*The prepare phase in the transaction is the phase where data is viewed, whereas the execute phase of the transaction is the phase where the data is modified.*

## 4. This is the hardest quest so far, so if it takes you some time, do not worry! I can help you in the Discord if you have questions.

### -Add two new things inside your contract:

#### -A variable named myNumber that has type Int (set it to 0 when the contract is deployed)

#### -A function named updateMyNumber that takes in a new number named newNumber as a parameter that has type Int and updates myNumber to be newNumber

![Screen Shot 2022-04-28 at 11 04 40 PM](https://user-images.githubusercontent.com/104539205/165883754-5ca1b110-a758-4146-8992-dcc50936b003.png)

### -Add a script that reads myNumber from the contract

![Screen Shot 2022-04-28 at 11 04 56 PM](https://user-images.githubusercontent.com/104539205/165883774-3057e056-017f-4ed5-b15c-567e41fa656c.png)

### -Add a transaction that takes in a parameter named myNewNumber and passes it into the updateMyNumber function. Verify that your number changed by running the script again.

![Screen Shot 2022-04-28 at 11 05 13 PM](https://user-images.githubusercontent.com/104539205/165883793-d6d481fc-096f-41e9-86cd-3daf561d9287.png)

![Screen Shot 2022-04-28 at 11 05 36 PM](https://user-images.githubusercontent.com/104539205/165883809-d6d41e9e-17fb-4a21-ab29-0c0378a00d40.png)
