# ReactTry
## 紀錄學習React 遇到的各種筆記

### 重點觀念名詞
1. Single Page Applications。 
與之相對的則是Multi Page Applications，過往藉由按鈕等護界方式，在多個網頁間的切換，以此組成一個網站．  
SPA將所有資料放在同一頁面，不需重新載入，使用經驗會更好．  

2. let 和 const的差別  
let：let 是用來宣告可被重新賦值的變數。  
const：const 是用來宣告不可被重新賦值的變數。  
```Javascript
let name = 'John';
name = 'Jane'; // 合法

const name = 'John';
name = 'Jane'; // 錯誤，不能重新賦值

const arr = [1, 2, 3];
arr.push(4); // 合法
arr = [5, 6, 7]; // 錯誤，不能重新賦值

const obj = { name: 'John' };
obj.name = 'Jane'; // 合法
obj = { name: 'Jane' }; // 錯誤，不能重新賦值
```

3. Arrow Function  
Arrow function（也稱為箭頭函式）是 JavaScript 中的一種函式，它的語法簡潔，並且會綁定 this。  
例如以下兩者的功能是相同的  
```Javascript
function add(a, b) {
  return a + b;
}
const add = (a, b) => a + b;
```

4. React in "Declarative way"  
Declarative 宣告式 vs. Imperative 命令式是兩種相對應的邏輯  
Declarative是聲明你需要甚麼（What），不用理會程式用甚麼方法、甚麼步驟做到。  
而React就是我們定義需要的狀態，讓React自行渲染出對應的Javascript Dom！  
```JavaScript
//藉由React協助用戶創鍵對應Html語法
<Btn 
  onToggleHighlight={this.handleToggleHighlight}
  highlight={this.state.highlight}>
    {this.state.buttonText}
</Btn>
```
Imperative是告訴程式如何做（How）一些事，其實就是平日programming常做的，你寫下指示，程式一步一步跟隨你的指示做。  
```JavaScript
//實際定義每一步驟及條件要做些什麼
$("#btn").click(function() {
  $(this).toggleClass("highlight")
  $(this).text() === 'Add Highlight'
    ? $(this).text('Remove Highlight')
    : $(this).text('Add Highlight')
})
```
(Chapter.13 會講解為何使用classs component)

5. JSX
是一個允許在JavaScript下撰寫Html的擴充功能，藉由{}將目標包起來，便可以實現其功能，   
達到更簡單的建立複雜的UI物件
```JavaScript
// const 為常數
const lists = ['JavaScript', 'Java', 'Node', 'Python'];

class HelloMessage extends React.Compoent {
  render() {
    return (
    <ul>
      {lists.map((result) => {
        return (<li>{result}</li>);
      })}
    </ul>);
  }
}
```

6. DOM(Document Object Model)   
DOM（文檔對象模型）是一種結構化文檔的模型, 用於將文檔內容表示為一棵樹，其中每個节点都表示文檔中的一個元素或屬性。   
通過使用 DOM，您可以使用 JavaScript 代碼操作瀏覽器中的網頁元素，例如修改元素的文本、屬性或樣式.  

7. Controlled components Vs un-controlled components  
Controlled components 是指，組件的狀態（state）是由父組件控制的。在 controlled components 中，組件的表單輸入值也是由父組件控制的。這意味著，如果要更改組件的值，必須在父組件中更改組件的 state，並使用 props 將新值傳遞到子組件中。   

Un-controlled components 是指，組件的狀態是由自己維護的。在 un-controlled components 中，組件的表單輸入值也是由自己維護的。這意味著，組件可以通過監聽表單輸入事件並使用 DOM API 來更新自己的值 Ex. useRef()。   
```Javascript
// Controlled component for email input
const EmailInput = ({ value, onChange, onBlur }) => {
  return (
    <input
      type="email"
      value={value}
      onChange={onChange}
      onBlur={onBlur}
      required
    />
  );
};

```
### React運作原理
![image](https://user-images.githubusercontent.com/24216536/210242719-fbbf2ad9-7de4-4589-bdad-393a871ab340.png)。  
React-> 一套Javascript Library, 允許使用者建立前端介面，並且透過ReactDOM與WEB實際進行互動。  
React背後的運作總是圍繞著Components進行．Props(parent傳入資料), Context(Component內定義的數據), State(Component內的可變量數據)，並透過Real DOM渲染出使用者看到的畫面．
![image](https://user-images.githubusercontent.com/24216536/210243971-19cad863-4588-4426-b5fb-fea1ffc87cd6.png)   
且當Compoenets改變時React會Re-Evaluating, 而不會Re-Rendering Real DOM，此特性會讓效能提升，不需要一直重新渲染畫面．   

* Component Re-Evalusting example
當點擊Button後可以看到多出現一行*APP RUNNUNG*, 且觀察Element葉簽下，只有<p>TAG進行更新其餘畫面內容不變～。  
```Javascript
function App() {
  const [showParagraph, setShowParagraph] = useState(false);

  console.log('APP RUNNING');
  
  const toogleParagraphHandler = () => {
    setShowParagraph((prevShowParagraph) => !prevShowParagraph);
  };
  return (
    <div className="app">
      <h1>Hi there!</h1>
      {showParagraph && <p>This is new!</p>}
      <Button onClick={toogleParagraphHandler}>toggle Paragraph</Button>
    </div>
  );
}
```
![image](https://user-images.githubusercontent.com/24216536/210246719-0708bdfc-b3cf-4826-b9c5-2a4eccd62a10.png)。 
![image](https://user-images.githubusercontent.com/24216536/210246734-c3ad08e6-b39e-4f14-9ebc-2fa8ef979eac.png)。   

Component Re-Evalusting exampleComponent Re-Evalusting exampleComponent Re-Evalusting exampleComponent Re-Evalusting exampleComponent Re-Evalusting examplefaowejifoaweffdsfdsfComponent Re-Evalusting example* 


React DOM 是一個模組，用於在 React 中操作 DOM。它提供了許多函數，用於在 React 中渲染、修改和刪除 DOM 元素。
### React語法研究
1. useState-狀態  
React state 是 React 中用來儲存、更新和管理Component的狀態的一個重要概念。   
在 React 中，Component的狀態是一個 JavaScript 物件，它可以在組件的生命週期中隨時更新。當組件的狀態改變時，React 會自動重新渲染組件，並使用最新的狀態更新 UI。  
```JavaScript
//其中的filteredYear即是預設值為2020並利用ExpensesFilter該Component下拉選單，用作對state的更新．  
const Expenses = (props) => {
  const [filteredYear, setFilteredYear] = useState('2020');

  const filterChangeHandler = (selectedYear) => {
    setFilteredYear(selectedYear);
  };

  return (
    <div>
        <ExpensesFilter
          selected={filteredYear}
          onChangeFilter={filterChangeHandler}
        />
    </div>
  );
};
```

2. useEffect  
主要功能-> Render UI, React to User Input
useEffect接收兩個參數，第一個是一個函式，定義componentDidMount或componentDidUpdate要做什麼事，此函式的回傳值也要是一個函式，表示componentWillUnmount 要做什麼事。   
第二個參數是一個array，裡面是定義當哪些變數被改變時，這個useEffect要重新被觸發，若為空時則代表只會執行一次。   
主要可以實作出 componentDidMount(不帶第二個參數)、componentDidUpdate(第二個參數被改變時)、componentWillUnmount(return時做) 三個生命週期函式。  
```Javascript
const testEffect = () => {
console.log('invoke function component');

useEffect(() => {
console.log('execute function in Effect');
});

return(
<div>
{console.log('render');}
</div>
);
}
```
在網頁的Console會得到如下的順序，1. Invoke function component-> 2. render-> 3. execute Effect
<img width="649" alt="image" src="https://user-images.githubusercontent.com/24216536/209051557-0986390a-c9d9-4bdd-942a-cd193295ec1a.png">


3. Css 管理 
在 React 專案內如果沒有使用 styled component 或者 CSS module 將樣式區隔的話，所有樣式都是 global（意思是所有 component 都會吃到），為了解決這個問題，便出現 styled component / CSS module。  

styled component      
在 component 內引入 styled component，並切記需要把 styled component 放在 function component 之外（不要放在 function component 內宣告），因為這樣子會造成 component re-render 時重複建立 styled component，這麼做會造成 render 的速度下降。   

Props 的傳遞：
styled component 會自動接受該 component 上有的 props，透過函式的方式 styled component 可以取得傳入 component 的 props
```Javascript
const Button = styled.button`
  /* Adapt the colors based on primary prop -> 用 arrow function 取得傳入的 props，即可依照需求動態地顯示樣式 */
  background: ${props => props.primary ? "palevioletred" : "white"};
  color: ${props => props.primary ? "white" : "palevioletred"};

  font-size: 1em;
  margin: 1em;
  padding: 0.25em 1em;
  border: 2px solid palevioletred;
  border-radius: 3px;
`;

render(
  <div>
    <Button>Normal</Button>
    /** 傳入 props -> primary */
    <Button primary>Primary</Button>
  </div>
);
```
CSS Modules - A CSS Module is a CSS file in which all class names and animation names are scoped locally by default. 
-> 可以讓你使用模組化的方式來管理樣式表，並使用 JavaScript 導入該模組。每個模組都有自己的namespace，所以你可以在多個模組中使用相同的樣式名稱，而不用擔心命名衝突的問題。  
優點
- 確保單個組件（元件）的所有樣式集中在同一個地方.  
- 確保元件樣式只應用於該組件.  
- 解決 CSS 全局作用域的問題.  

比較乾淨的作法，因為 style 還是存在於 style sheet 中，不會和 component 擠在同一個 file 內   
style sheet 的檔名需要修改成 componentName.module.css/scss  
有別於直接 import './style.css'，需要給 style sheet 一個變數  
import styles from './componentName.module.css（或者是用 import classes from './componentName.module.css'  
此時就可以直接用物件取值的方式使用 style class  
編譯完顯示在 DOM 上會是 ComponentFileName_styleClassName__hash  
```javascript
// Component.js

import styles from './componentName.module.css'

// ...

{
  return (
    <>
      // {} -> expression 所以可以用 template literal
      <MyComponent className={`${styles.title}}`}/>
      // dot notation 不可以用特別符號，有特別符號的需求就需要用 bracket notation
      <MyComponent className={`${styles['my-class']}`}/>
    </>
  )
}
```
4. Wrapper Component, React.Fragment.  
當很多層div包再一起會使html架構變得難以閱讀(div soup).  
```Javascriipt
const Wrapper = props => {
 return props.children;
}
export default Wrapper;
```  
除了自己寫一個新的Component也可以使用React.Fragment來代表Empty Wrapper component.  
```Javasciprt
    <React.Fragment>
      <h1>Title</h1>
      <p>Paragraph</p>
    </React.Fragment>
or
      <>
      <h1>Title</h1>
      <p>Paragraph</p>
    </>
```
5. React Portals.  
React portals 是一種特殊的技術，用於將 React 組件渲染到 DOM 結構的任何位置。它們可以用於解決在 React 中無法將元素渲染到某些 DOM 元素中的限制。   

要在 React 中使用 portals，需要使用 ReactDOM.createPortal 函數。該函數接受兩個參數：要渲染的組件和要將其渲染到的 DOM 元素(使用Dom API進行操作Ex. document.getElementById())。   
```Javascript
<React.Fragement>
 {ReactDom.createPortal(<Backdrop onClick= {props.onConfirm} />,document.getElementById('backdrop-root') )}
</React.Fragment>
```
6. useRef.  
reference，在程式中一般是指"變數指向的記憶體位置上對應到的值"。 
useRef是一個函式，跟useState一樣接收一個參數，作為變數初始值。差別是useRef回傳的是一個物件，裡面只有一個屬性current.   
React會確保useRef回傳出來的這個物件不會因為React元件更新而被重新創造。也就是說在你初始化過後，這個物件會始終指向同一個reference。 
並且永遠都可以利用current.value來讀取此ref的值。  
```Javascript
const inputRef = useRef();
 <input type="text" ref={inputRef} />
```
常用於.  
* 以原生方式操作DOM元素.  
* counter變數.  

7. useReducer.  
類似於useState的狀態管理Hook但可以實現更複雜的條件管理。   
```const [state, dispatch] = useReducer(reducer, initialState, initStateFn);```.  
* 第一個參數用來設定變更 state 的規則，指定發生特定的 action 時如何更新 state   
* 第二個參數是初始化當下的 state   
* 第三個參數是初始化 state 的函式，非必要的參數  
* dispatch 用來觸發 action  
推薦用於當State的變化與其他State進行掛勾時，使用Reducer將兩者的變化包再一起進行管理會更方便。   

```Javascript
import React, { useReducer } from "react";
+
// 初始化 state
const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    case "reset":
      return { count: (state.count = 0) };
    default:
      return { count: state.count };
  }
}

export default function App() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      Count: {state.count}
      <br />
      <br />
      <button onClick={() => dispatch({ type: "increment" })}>Increment</button>
      <button onClick={() => dispatch({ type: "decrement" })}>Decrement</button>
      <button onClick={() => dispatch({ type: "reset" })}>Reset</button>
    </div>
  );
}
```
Reducer vs State  
簡單的場景優先使用State, 較多複合條件則選擇使用Reducer來降低程式碼的複雜度。 
![image](https://user-images.githubusercontent.com/24216536/209511537-2a79a6cd-4b6d-4fa3-97fd-18026e95b82e.png)  

8. useContext.  
當需要使用的State於越來越多層之間傳遞時，就會更難以管理他們，因為很Props僅是需要經過中間件的傳遞進到Component中，造成了很多的傳遞管理困難．   
就可以利用useContext來進行全域的參數傳遞.  

9. Hooks使用注意事項.  
![image](https://user-images.githubusercontent.com/24216536/209531771-a10e0046-2ad1-4290-97f3-38ddc07572e0.png).  

10. useImperativeHandle.  
先前有提到若是有focus 在 input 元素之類的需求，可以透過 useRef 的方式達成。  
但如果今天這個 input 元素是額外再封裝成一個 component 的話，而父 component 也想要對於這個被額外封裝成 component 的 input 元素可以執行像是 focus 的需求的話，那這時候就還需要用到 useImperativeHandle 這個 Hook.   
並透過forwardRef 用來建立一個新的 React component 並將 ref 屬性轉交到底下的另外一個component。
```Javascript
const CustomTextInput = React.forwardRef((props, ref) => {
  const inputRef = useRef(null);

  useImperativeHandle(ref, () => ({
    focus: () => {
      inputRef.current.focus();
    },
    getValue: () => inputRef.current.value
  }));

  return <input ref={inputRef} />;
});

const ParentComponent = () => {
  const inputRef = useRef(null);

  const handleClick = () => {
    inputRef.current.focus();
    console.log(inputRef.current.getValue());
  };

  return (
    <div>
      <CustomTextInput ref={inputRef} />
      <button onClick={handleClick}>Focus and log value</button>
    </div>
  );
};
```
10. IMG Import
```javascript
import mealsImage from '../../assets/meals.jpg
<img src={mealsImage}></img>
```

11. 傳入input var
利用...props.input可以將類似type:'text'這樣子的參數自動帶入input tag內
```<input {...props.input}/>```
