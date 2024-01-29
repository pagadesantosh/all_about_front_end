### Composition:

- is smaller pieces that are combined to create something bigger
- Lot of people prefer composition over inheritance

```js
// Amazon shopping
const user = {
  name: 'Kim',
  active: true,
  cart: [],
  purchases: [],
};
const amazonHistory = [];
const compose =
  (f, g) =>
  (...args) =>
    f(g(...args));
purchaseItem(
  emptyCart,
  buyItem,
  applyTaxToItems,
  addItemToCart
)(user, { name: 'laptop', price: 200 });

function purchaseItem(...fns) {
  return fns.reduce(compose);
}

function addItemToCart(user, item) {
  amazonHistory.push(user);
  const updateCart = user.cart.concat(item);
  return Object.assign({}, user, { cart: updateCart });
}

function applyTaxToItems(user) {
  amazonHistory.push(user);
  const { cart } = user;
  const taxRate = 1.3;
  const updatedCart = cart.map((item) => {
    return {
      name: item,
      price: item.price * taxRate,
    };
  });
  return Object.assign({}, user, { cart: updatedCart });
}

function buyItem(user) {
  amazonHistory.push(user);
  return Object.assign({}, user, { purchases: user.cart });
}

function emptyCart(user) {
  amazonHistory.push(user);
  return Object.assign({}, user, { cart: [] });
}

/*
   Implement a cart feature:
     1. Add items to cart.
     2. Add 30% tax to item in cart.
     3. Buy item: cart --> purchases.
     4. Empty cart

   Bonus:
     Accept refunds.
     Track user history.
  */
```

----


### Inheritance:

- is a super class that is extended to smaller pieces that add or overwrite things.
- With Inheritance we have tight coupling problem, because your subclass(child classes) are using parent classes (Making one change in parent can break in subclasses )

```js
class Character{
    constructor(name, weapon){
        this.name = name;
        this.weapon = weapon
    }
    attack(){
        return 'attack with ' + this.weapon
    }
}

class Elf extends Character{
    constructor(name, weapon type){
        super(name, weapon)
        console.log('what am i?', this)
        this.type = type
    }
}

class Ogre extends Character{
    constructor(name, weapon, color){
        super(name, weapon);
        this.color = color
    }
}

````


#### Inheritance is a super class that is extended to smaller pieces that add or overwrite things.
![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/ff817528-1a70-4bf1-84b0-2d1a46fa061a)

#### Smaller pieces combined to something bigger.
![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/b1d55e65-9c15-4354-8cda-31a6adf8907b)

-----

Example usage on how to convert the Inheritance logic to much reusability for future proof

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/458009e5-278d-4382-a714-9e1ff7082f2a)
