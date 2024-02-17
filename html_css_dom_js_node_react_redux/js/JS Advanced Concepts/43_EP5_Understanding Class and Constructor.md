```js
class CreateCustomer {
  constructor(name, accountBalance, branch) {
    this.name = name
    this.accoutnBalance = accountBalance
    this.branch = branch
  }
  addMoney() {
    this.accountBalance++
  }
  fetchBalance() {
    console.log("The balance is " + this.accountBalance)
  }
}

const customer1 = new CreateCustomer("Alex", 100, "XYZ")
customer1.addMoney()
customer1.fetchBalance()
```

#### Functions vs class Code

<img width="632" alt="image" src="https://user-images.githubusercontent.com/42731246/215966609-89576904-480b-423e-8a20-cbd4a0dee6f7.png">

#### Labels Function and Object part as a class, in function part it stores the constructor, and everything else is executed same

<img width="532" alt="image" src="https://user-images.githubusercontent.com/42731246/215967029-be93a4d3-a75a-4d1e-bae4-b1429f158893.png">
