
#### 什麼是TypeScript ?
TypeScript 是加強版的JavaScript (超集 Superset)，加強了 Type 的部分，讓開發者在編寫程式時可以指定變數的類型，讓變數保持一致的類型，有助於減少錯誤，以及提高程式碼的穩定性和可讀性。

TypeScript 在編譯階段可以做型別檢查，發現型別錯誤，但即使 TypeScript 編譯報錯，也可以產生 JavaScript 檔案

#### 常見型別
- 基礎型別：`boolean`、`number`、`string`、`null`、`void`、`undefined`、`symbol`
- 物件型別：`array`、 `function`、`object`、`Tuple`、`interface`、`enum`、`class`
- 特殊型別：`any`、`never`、`unknown`

### 用法

#### Array 
```ts
let list: number[] = [1, 2, 3];  
let list: Array<number> = [1, 2, 3]; // 等同於上面的寫法  
  
let list: readonly number[] = [1, 2, 3]; // 不能修改 Array 裡的元素  
let list: ReadonlyArray<number> = [1, 2, 3]; // 等同於上面的寫法
```

#### Tuple 元組

有固定長度和元素型別的陣列
```ts
let tuple: [number, string, boolean, number] = [3, 'foo', true, 10]; 
tuple = [4, 'bar', false, 30];

//Readonly  Tuple (可在定義陣列時加上 as const)
// 如此就會是固定值的 readly tuple ，沒加的話則會是 string[]
const phoneBrand = ['apple', 'samsung', 'xiaomi', 'sony'] as const;
```

#### Enum 列舉
通常用來管理多個**同系列**的常數（不可修改的變數），做為狀態的判斷所使用，比如一週只能有七天。
```ts
enum Days {Sun, Mon, Tue, Wed, Thu, Fri, Sat};
// 在 Enum 中的每個常數都可以經由 `=` 指定 Value，若無則預設為 index 值
// 值可以是字串或數字
enum Days {
	Sun=0, 
	Mon=1, 
	Tue=2, 
	Wed=3, 
	Thu=4, 
	Fri=5, 
	Sat=6
};

console.log(Days.Sun === 0); // true
console.log(Days[0]); // Sun
```

#### Unknown
`unknown` 和 `any` 一樣，該型別的變數都可以帶入任意的值（屬於 Top Types），但有一個關鍵的差異在於，開發者不能對 `unknown` 型別的變數進行任何操作，但 `any` 可以
```ts
let isAny: any;  
let isUnknown: unknown;  
  
isAny.hello(); // 可以對 any 型別進行任何操作  
isUnknown.hello(); // 不可以對 unknown 型別進行任何操作
```

####  Any 
`any` 和 `never` 相反，可以把 `any` 視為什麼都包含在內的全集合（Universe），它包含了所有可能性。

一開始宣告變數時，如果對變數不設值，且為註記型別，都會被視為是 any：

```ts
let foo; // any
type A = 'string' | 'number' | any; // type A = any
```

#### Never 
- never 使用的時間點是該函式會「卡在裡出不來」例如，無窮迴圈；或者「終止在函式裡」，例如，拋出錯誤
- never 是用來提醒開發者，這個函式執行後，程式將無法繼續往後執行。
```ts
// never 就是一個空  
type A = 'string' | 'number' | never; // type A = "string" |"number"  
  
// never 也屬於 any  
type T = never extends any ? true : false; // type T = true
```


#### Type Assertions 型別斷言

用於告訴 TypeScript 編譯器你比它更了解某個值的型別，通常在處理複雜或不確定的情況下使用。Type Assertions 有兩種主要的用法，一種是使用角括弧（`<>`），一種是用 `as`

```ts
const data = JSON.stringify({  
	foo: 'foo',  
	bar: 'bar',  
});  
  
// 使用 <> 進行 type assertions  
let parsedJSON1 = <{ foo: string; bar: string }>JSON.parse(data);  
  
// 使用 as 進行 type assertions  
let parsedJSON2 = JSON.parse(data) as { foo: string; bar: string };
```

也可以搭配 Type Alias 使用：
```ts
type Data = {  foo: string;  bar: string;};

// 使用 <> 進行 type assertions
let parsedJSON1 = <Data>JSON.parse(data);
// 使用 as 進行 type assertions
let parsedJSON2 = JSON.parse(data) as Data;
```

[[Utility Types]]

