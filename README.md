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
### React語法研究
1. State-狀態  
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
