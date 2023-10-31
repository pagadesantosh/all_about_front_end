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
  const customer = Object.create(functionsBundle);
  customer.name = name;
  customer.accountBalance = accountBalance;
  customer.branch = branch;
  return customer;
}

const customer1 = createCustomer('Alex', 100, 'XYZ');
customer1.addMoney();
customer1.fetchBalance();

const salariedUserFunctions = {
  fetchSalary: function () {
    console.log('The salary is ' + this.salary);
  },
};

function createSalariedUser(name, accountBalance, branch, salary) {
  const salariedUser = createCustomer(name, accountBalance, branch);
  Object.setPrototypeOf(salariedUser, salariedUserFunctions);
  salariedUser.salary = salary;
  return salariedUser;
}

Object.setPrototypeOf(salariedUserFunctions, functionsBundle);
const customer2 = createSalariedUser('Jane', 100, 'XYZ', 10);
customer2.addMoney();
customer2.fetchBalance();
customer2.fetchSalary();
```

---

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/f12174f7-b46f-4928-8c9c-182ce60fa3cc)

**Object.setPrototypeOf** : Allows us to change proto reference of the first argument and it assigns it reference to the second argument

```js
Object.setPrototypeOf(salariedUserFunctions, functionsBundle);
```

For Ex: First argument is salariedUserFunctions, second argument is functionsBundle, so `salariedFunctions Proto will be referenced to the functionsBundle`

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/84f3df96-12ce-43c7-a40f-605d0582f761)