```ts
// Func with optional arg
const createPassword = (name: string, age?: number):string => `${name}${age}`;
// отсутствующий арг можем обработать уже внутри функции
```

```ts
// REST 
const createSkills = (name: string, ...skills: Array<string>):string => 
								`${name}, my skills are ${skills.join('')}`;
createSkills('Jack', 'JS', 'ES6', 'React');
```

```ts
// Void
const greetUser = (): void => {
	alert('Hello, nice to see you!');
};

// Never Type
const msg = 'hello';
const error = (msg: string): never => {
	throw new Error(msg);
};

const infiniteLoop = (): never => {
	while(true) {}
};
```

```ts
// Describe fn type
let myFunc: (firstArg: string) => void;

function oldFunc(name: string): void {
	alert(`Hello ${name}, nice to see you!`);
};

myFunc = oldFunc;
```