### **1. let and const keywords **
### **2. Arrow Functions**
### **3. Multi-line Strings**

We can create multi-line strings by using back-ticks(\`).  

```jsx
let greeting = `Hello World,     
                Greetings to all,
                Keep Learning and Practicing!`
```

### **4. Default Parameters**

```jsx
//ES6
let calculateArea = function(height = 100, width = 50) {  
    // logic
}

//ES5
var calculateArea = function(height, width) {  
   height =  height || 50;
   width = width || 80;
   // logic
}
```

### **5. Template Literals**

```jsx
let name = `My name is ${firstName} ${lastName}`
```

### **6. Destructuring Assignment**

Помогает доставать значения из массивов, или св-ва из объектов.

```jsx
//Array Destructuring
let fruits = ["Apple", "Banana"];
let [a, b] = fruits; // Array destructuring assignment
console.log(a, b);

//Object Destructuring
let person = {name: "Peter", age: 28};
let {name, age} = person; // Object destructuring assignment
console.log(name, age);
```

### **7. Enhanced Object Literals**

Можно легко создать объект с пропсами внутри curly braces.

```jsx
function getMobile(manufacturer, model, year) {
   return {
      manufacturer,
      model,
      year
   }
}
getMobile("Samsung", "Galaxy", "2020");
```

### **8. Promises**

[[Promise]]

### **9. Classes**

Раньше в JS классов не было, теперь мы можем использовать классы, похожие на то что используется в других языках программирования (работают они не точно также). Можем создавать объекты, наследовать с помощью extends и тд

```jsx
class UserProfile {   
   constructor(firstName, lastName) { 
      this.firstName = firstName;
      this.lastName = lastName;     
   }  
    
   getName() {       
     console.log(`The Full-Name is ${this.firstName} ${this.lastName}`);    
   } 
}
let obj = new UserProfile('John', 'Smith');
obj.getName(); // output: The Full-Name is John Smith
```

### **10. Modules**

Можно разделять код по модулям (отдельный .js файл) и использовать import/export для расшаривания. 

```jsx
export var num = 50; 
export function getName(fullName) {   
   //data
};
```

```jsx
import {num, getName} from 'module';
console.log(num); // 50
```