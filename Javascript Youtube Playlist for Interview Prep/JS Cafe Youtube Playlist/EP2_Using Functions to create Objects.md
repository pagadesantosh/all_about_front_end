##### Basic Approach (which we need to avoid)

```js
//Approach 1
const customer1 = {
  name: 'Alex',
  accountBalance: 100,
  branch: 'HDFC XYZ',
  addMoney: function () {
    customer1.accountBalance++
  },
}
customer1.addMoney()
console.log(customer1.accountBalance)

//Approach 2
const customer2= {}
customer2.name = "Jane"
customer2.accountBalance = 200;
customer2.branch = "ICICI XYZ";
customer2.addMoney: function (){
    customer2.accountBalance++;
}
customer2.addMoney();
console.log(customer2.accountBalance)
```

---

##### Function to create Objects

```js
function createCustomer(name, accountBalance, branch){
const customer =  {}
customer.name = name
customer.accountBalance = accountBalance
customer.branch =branch
customer.addMoney: function (){
    customer.accountBalance++;
}
return customer;

}

const customer1 = createCustomer("Alex", 100, "XYZ")
const customer2 = createCustomer("Jane", 200, "XYZ-2")

customer1.addMoney()
console.log(customer1.accountBalance)

```

![image](https://user-images.githubusercontent.com/42731246/215371199-2dd3dc04-c636-46dd-8455-145724482b8b.png)

<strong>return of the customer points out to the Global memory </strong>
![image](https://user-images.githubusercontent.com/42731246/215371372-1413d3d9-1ec9-41c4-8a69-8a88817ea01c.png)

<strong>Flaw with this approach is it creates copies of the `addMoney function` </strong>which is not a good idea if there are lakhs of customers

![image](https://user-images.githubusercontent.com/42731246/215371513-7f14aba3-ab96-4e1e-b351-174e8e5d9645.png)

- Instead of having copies of addMoney function in every object <strong>if they can somehow referece to a very common source of this addMoney function</strong> so that we can avoid having multiple copies in every object and have that function in one place.

![image](https://user-images.githubusercontent.com/42731246/215371865-ce57fe9e-82b2-4c5f-b21b-1f81b5958bfc.png)

---

### Code to avoid multiple copies of addMoney function

```js
const functionsBundle = {
  addMoney: function () {
    this.accountBalance++;
  },
  fetchBalance: function () {
    console.log('The balance is ' + this.accountBalance);
  },
};

function createCustomer(name, accountBalance, branch) {
  //we are creating an empty object with the prototype of functionsBundle and that is why it references to addMoney and fetchBalance
  const customer = Object.create(functionsBundle);
  customer.name = name;
  customer.accountBalance = accountBalance;
  customer.branch = branch;
  return customer;
}

const customer1 = createCustomer('Alex', 100, 'XYZ');
customer1.addMoney();
customer1.fetchBalance();
```

#### Code walkthrough:

- Whenever we use Object.create(), it always returns the empty object. (in our case it is customer which is empty object)
- Object.create() attaches the proto of the object returned with the argument
  ![image](https://github.com/saiteja-gatadi1996/Infinite-scroll-of-Images-API---React/assets/42731246/3f88cd66-d3db-4ea5-a743-36feb89b814e)

- We are passing functionsBundle as the argument to the Object.create(), so the proto points to the functionsBundle (see below)

![image](https://user-images.githubusercontent.com/42731246/215372673-57360878-8893-4a9d-bafb-ce4508e65b2f.png)

- Adding properties to the createCustomerObject and we are doing a return
  ![image](https://user-images.githubusercontent.com/42731246/215372788-df672cb8-6424-4af3-ae43-f87a54ea0bef.png)

- this return keyword says that we are returning the customer object to the customer1 and this proto referencing to the functionsBundle

![image](https://user-images.githubusercontent.com/42731246/215373096-c7b35bf1-f73e-4c6b-8a87-29f0ba44d708.png)

---

- Whenever we do customer1.addMoney(), it checks in the customer1 object and as it doesn't find there it goes to the proto way up to the functionsBundle and here it finds the addMoney function and it executes

![image](https://user-images.githubusercontent.com/42731246/215373320-d292ff7b-4ff1-4e4b-8685-ce5e1407f0a6.png)
