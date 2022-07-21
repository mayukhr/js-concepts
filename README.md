# js-concepts

#### 1. What is Event delegation?
We add event listener to a parent instead of specific nodes. 
As an example if we have soemthing like: 
```
<ul> //add onclick on this, instead of adding it to li items
  <li id = 'item-1'/>
  <li id = 'item-2'/>  // clicked this item  
  <li id = 'item-3'/>  
</ul>
```
to check which <li> is clicked, we can do, `e.target.id` which will give `item-2`
  
#### 2. How 'this' works in js?
  
	https://codeburst.io/the-simple-rules-to-this-in-javascript-35d97f31bde3
	
 - for `arrow` functions, this is Surrounding scope at the time of creation.
  Ex: 
  ```
  hello = () => {
   return this; //window object.
  }
  ```
  
  - If the `new` keyword is used when calling the function, `this` inside the function is a brand new object.
  ```
  function Fruit(color, taste, seeds) {
    console.log(this); // Fruit {color: "Yellow", seeds: 1, taste: "Sweet"}

    this.color = color;
    this.taste = taste;
    this.seeds = seeds;
}
  
// Create an object
const fruit1 = new Fruit('Yellow', 'Sweet', 1);
  ```
- If apply, call, or bind are used to call/create a function, this inside the function is the object that is passed in as the argument.
 
```
  function Car(type, fuelType){
	this.type = type;
	this.fuelType = fuelType;
  }

function setBrand(brand){
	Car.call(this, "convertible", "petrol");
	this.brand = brand;
	console.log(`Car details = `, this);
}

function definePrice(price){
	Car.call(this, "convertible", "diesel");
	this.price = price;
	console.log(`Car details = `, this);
}

const newBrand = new setBrand('Brand1');
{
  brand: "Brand1",
  fuelType: "petrol",
  type: "convertible"
} 
const newCarPrice = new definePrice(100000);
  {
  fuelType: "diesel",
  price: 100000,
  type: "convertible"
} 
  ```
 - If a function is called as a method, such as obj.method() — this is the object that the function is a property of.
 - If a function is invoked as a free function invocation, meaning it was invoked without any of the conditions present above, this is the global object. In a browser, it is the window object. If in strict mode ('use strict'), this will be undefined instead of the global object.
 - If multiple of the above rules apply, the rule that is higher wins and will set the this value.
