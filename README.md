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

	
	
#### 3. What is prototypal inheritance?
	
	```
		function Animal(name) {
		  this.name = name;
		}

		Animal.prototype.status = function (){
		  return `${this.name} is sleepy!`;
		}

		function Gorilla(name) {
		  Animal.call(this, name);
		  this.name = name;
		}

		Gorilla.prototype = Object.create(Animal.prototype);
		Gorilla.prototype.eyeColor = function () {
		  return `${this.name} has red eyes!`;
		}

		const anim = new Animal('random');
		const gorr = new Gorilla('white Gorilla');

		console.log(gorr)
	
	```

	
#### 4. Write polyfill of map() | How to call it using call()?
	
	```
		 const  mapj = function (callback) {
		  let inputArr = this;
		  if(inputArr instanceof Array) {
		    let result = [];

		    for(item of inputArr) {
		      result.push(callback(item))
		    }
		    return result;
		  }
		  else {
		    throw new Error (`${inputArr} is not an array`)
		  }
		}
		Array.prototype.mapj = mapj;
		// let b = [1,2,3].mapj(a=>a*a);

		let c=mapj.call([2,3,4], a=>a*a)// call( this, ...args )
		let d = mapj.apply([2,3,4], [a=>a*a])
		let e = mapj.bind([2,3,4], a=>a*a);
	```
	
#### 5. Write polyfill of filter()
	
	```
		const filterj = function (callback) {
		  const res = [];
		  for(let item of this) {
		    if(callback(item))
		      res.push(item)
		  }
		  return res;
		}

		let b = [1,2,3,48888,'bbijbiiiiiib'].filter(a=>a.length>3)

		console.log(b)
	```
	
###4. mergeSort 
	
	```
		function mergeSort (arr) {
		  if (arr.length === 1) {
		    // return once we hit an array with a single item
		    return arr
		  }

		  const middle = Math.floor(arr.length / 2) // get the middle item of the array rounded down
		  const left = arr.slice(0, middle) // items on the left side
		  const right = arr.slice(middle) // items on the right side

		  return merge(
		    mergeSort(left),
		    mergeSort(right)
		  )
		}

		// compare the arrays item by item and return the concatenated result
		function merge (left, right) {
		  let result = []
		  let indexLeft = 0
		  let indexRight = 0

		  while (indexLeft < left.length && indexRight < right.length) {
		    if (left[indexLeft] < right[indexRight]) {
		      result.push(left[indexLeft])
		      indexLeft++
		    } else {
		      result.push(right[indexRight])
		      indexRight++
		    }
		  }

		  return result.concat(left.slice(indexLeft)).concat(right.slice(indexRight))
		}

		const list = [2, 5, 1, 3, 7, 2, 3, 8, 6, 3]
		console.log(mergeSort(list)) 
							    
	```
###4. Simple Linked List traversal

```
	class ListNode {
	  constructor(value, next) {
	    this.value = value;
	    this.next = next;
	  }
	}

	let ll = [5,4,3,2,1].reduce((acc, item) => new ListNode(item, acc), null)


	function traverse(head) {
	  let currentNode = head;
	  console.log(head)
	  while(currentNode) {
	    console.log(currentNode.value)
	    currentNode = currentNode.next;
	  }
	}

	traverse(ll);
```
