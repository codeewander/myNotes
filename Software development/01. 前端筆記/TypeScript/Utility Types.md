
#### 什麼是 Utility Types? 

Utility Types 會以「型別」作為 input，並且以另一個「型別」作為 output，也就是說，**Utility Types 就像函式一樣可以帶入 input 得到 output，透過 Utility Types 將可以「根據一個型別，來建立出另一個型別」**
#### Record
```ts
//Record<Keys, Type>：由特定的 key 和相同型別的值，產生的物件型別  
interface CatInfo {  
	age: number;  
	breed: string;  
}  

type CatName = 'miffy' | "boris";  

// key 只能是 miffy 或 boris 
// 值要符合 CatInfo 型別
let placeRecord: Record<CatName, CatInfo> = {  
	miffy: {  
		age: 10,  
		breed: 'Persian',  
	},  
	boris: {  
		age: 6,  
		breed: "Maine Coon",  
	},  
};
```

#### Pick 
```ts
// Pick<Type, Keys>：挑出特定屬性及其型別，變成新的物件型別   
interface Todo = {  
	title: string;  
	description: string;  
	completed: boolean;  
};  

// 從Todo中的屬性和型別，挑出 title 和 completed，創建新的 TodoPreview型別
type TodoPreview = Pick<Todo, 'title' | 'completed'>;  

// 等同於
 type TodoPreview = {  
	 title: string;   
	 completed: boolean;   
 }

const todo: TodoPreview = {
	title: "Clean room",
	completed: false
}
```

#### Omit 
```ts
// Omit<Type, Keys>：從物件中排除特定屬性及其型別，變成新的物件型別  
type Todo = {  
	title: string;  
	description: string;  
	completed: boolean;  
};  
// 從Todo中的屬性和型別，移除 title 和 completed，創建新的 TodoPreview 型別
type TodoPreview = Omit<Todo, 'title' | 'completed'>;  

// 等同於
 type TodoPreview = {  
	 description: string;  
 }

const todo: TodoPreview = {
	description: '123'
}
```

#### Partial 

```ts
// Partial<Type>：將 Type 內所有屬性設定為optional，變成新的物件型別  
type Todo = {  
	title: string;  
	description: string;  
};  
// 從Todo中所有屬性和型別設為Optional
type PartialTodo = Partial<Todo>;  

// 等同於 
type PartialTodo = {
	title?: string | undefined
	description? : string | undefined
}
```


#### Reference 
- [Utility Types](https://www.typescriptlang.org/docs/handbook/utility-types.html) @ TypeScript