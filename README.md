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
  
 - for `arrow` functions, this is Surrounding scope at the time of creation.
  Ex: 
  ```
  hello = () => {
   return this; //window object.
  }
  ```
  
  - If the new keyword is used when calling the function, this inside the function is a brand new object.
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
