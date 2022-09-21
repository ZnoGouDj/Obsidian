```ts
// Define object type
let user: { name: string, age: number } = {
	name: 'Egor', 
	age: 26,
};
```

💩💩💩💩💩💩💩💩
```ts
let user: { name: string, age: number, nickName: string } = {
	name: 'Egor',
	age: 26,
	nickName: 'znogoud',
};

let admin: { name: string, age: number, nickName: string } = {
	name: 'Max', 
	age: 20,
	nickName: 'dick'
}; // REPEAT TYPE DESCRIPTION! 
```

✅✅✅✅✅✅✅✅
```ts
type Person = { name: string, age: number, nickName: string };

let user: Person = {} 
let admin: Person = {}
```

If we have different fields:
```ts
// just add optional fields
type Person = {
	name: string, 
	age: number,
	nickName?: string,
	getPass?: () => string
}
```
Or we may extend:
```ts
type Person = {
	name: string, 
	age: number
};

type User = Person & { nickName: string }
type Admin = Person & { getPass: () => string }

// may use Interface as well

interface IAdmin extends IPerson {
	getPass: () => string
}
```

Sometimes you don’t know all the names of a type’s properties ahead of time, but you do know the shape of the values.
```ts
interface StringArray {
	[index: number]: string;
}
```