# 如何用JS做個計算器

今天要來講的是用`JavaScript`為網頁上的計算器賦予它計算的功能。  
我這邊是直接還原IPhone開啟內建計算器時的樣子。  
因此除了計算的功能之外，我也添加了一個顯示當下時間的功能。

[成品](https://reurl.cc/GXe11Z)



## HTML的部分

下面這邊是`HTML`中所有的代碼，我接下來分段落解說。  

```html
<div class="calculator">
    <div class="top-container">
        <div class="clock">
            <span class="hour"></span>:<span class="minute"></span>
        </div>
    <div class="status">
        <img src="status.png" alt="Status">
    </div>
    </div>
        <div class="value">0</div>
        <div class="buttons-container">
            <div class="button function ac">AC</div>
            <div class="button function pm">±</div>
            <div class="button function percent">%</div>
            <div class="button operator division">÷</div>
            <div class="button number-7">7</div>
            <div class="button number-8">8</div>
            <div class="button number-9">9</div>
            <div class="button operator multiplication">×</div>
            <div class="button number-4">4</div>
            <div class="button number-5">5</div>
            <div class="button number-6">6</div>
            <div class="button operator subtraction">−</div>
            <div class="button number-1">1</div>
            <div class="button number-2">2</div>
            <div class="button number-3">3</div>
            <div class="button operator addition">+</div>
            <div class="button number-0">0</div>
            <div class="button decimal">.</div>
            <div class="button operator equal">=</div>
        </div>
    <div class="bottom"></div>
</div>
```

### 時間
這邊是左上角的`時間`顯示。  

```html
<div class="clock">
    <span class="hour"></span>:<span class="minute"></span>
</div>
```

### 網路訊號與電量
這邊是右上角的`網路訊號`與`電量`顯示。  
這部分我能力不足，所以就用了張圖片稍微表示了一下。

```html
<div class="status">
    <img src="status.png" alt="Status">
</div>
```

### 運算數值
這邊是`運算數值`顯示。 

```html
<div class="value">0</div>
```

### 按鍵
這邊是`按鍵`顯示。 

```html
<div class="button function ac">AC</div>
<div class="button function pm">±</div>
<div class="button function percent">%</div>
<div class="button operator division">÷</div>
<div class="button number-7">7</div>
<div class="button number-8">8</div>
<div class="button number-9">9</div>
<div class="button operator multiplication">×</div>
<div class="button number-4">4</div>
<div class="button number-5">5</div>
<div class="button number-6">6</div>
<div class="button operator subtraction">−</div>
<div class="button number-1">1</div>
<div class="button number-2">2</div>
<div class="button number-3">3</div>
<div class="button operator addition">+</div>
<div class="button number-0">0</div>
<div class="button decimal">.</div>
<div class="button operator equal">=</div>
```

### 底部白色橫條
這邊是`底部白色橫條`顯示。 

```html
<div class="bottom"></div>
```

## CSS的部分
CSS的部分應該就不用多講了，這邊沒用到甚麼太特別的屬性。  
像`transform`這類的之前也都有講過，所以就不再多提了。  
這邊特別一點的應該就`grid網格布局`吧。  
我下面這邊就拉出來講一下。

```css
*{
    box-sizing:border-box;
    margin:0;
    padding:0;
    user-select:none;
}

body{
    font-family:"Helvetica Neue",sans-serif;
    margin:25px;
}

.calculator{
    background:black;
    border-radius:50px;
    color:white;
    height:1218px;
    padding:20px;
    position:relative;
    width:563px;
}

.top-container{
    display:flex;
    height:250px;
    justify-content:space-between;
    padding:0 20px;
}

.value{
    font-size:130px;
    font-weight:300;
    height:158px;
    margin-bottom:20px;
    margin-right:20px;
    text-align:right;
}

.buttons-container{
    display:grid;
    grid-gap:20px;
    grid-template-columns:repeat(4,1fr);
    grid-template-rows:repeat(5,1fr);
}

.button{
    align-items:center;
    background:#333;
    border-radius:50%;
    cursor:pointer;
    display:flex;
    font-size:45px;
    height:110px;
    justify-content:center;
    transition:filter .3s;
    width:110px;
}

.button.function{
    color:black;
    background:#a5a5a5;
}

.button.operator{
    background:#f1a33c;
}

.button.number-0{
    border-radius:55px;
    grid-column:1 / span 2;
    justify-content:flex-start;
    padding-left:43px;
    width:250px;
}

.button:active,
.button:focus{
    filter:brightness(120%);
}

.bottom{
    width:200px;
    height:5px;
    background:white;
    border-radius:4px;
    position:absolute;
    bottom:10px;
    left:50%;
    transform:translateX(-50%);
}
```

### grid網格布局
這邊我用`grid`的原因是我覺得用`flex`的話太麻煩了，要造出很多的`div`。  
之前剛好網路上找教學時看到有人用這個東西，所以就想說拿來用一下。 
   
從下面這段代碼，可以看到說我先設了一個`20px`的間距，套用在每一個網格。  
然後再將它分成`5行4列`。

```css
.buttons-container{
    display:grid;
    grid-gap:20px;
    grid-template-columns:repeat(4,1fr);
    grid-template-rows:repeat(5,1fr);
}
```

當然，`grid布局`不只有這樣，它可以對每條網線做到更多的調整。  
[這張圖片](https://i0.wp.com/yukihiew.com/wp-content/uploads/2021/08/2.600x400.png?w=601&ssl=1)可以讓你看個大概。  
我是看這篇[文章](https://yukihiew.com/about-css-grid/#:~:text=%E5%BC%B7%E5%A4%A7%E7%9A%84CSS%20grid%E7%B6%B2%E6%A0%BC%E6%8E%92%E7%89%88-%E4%BB%8B%E7%B4%B9%E8%88%87%E6%87%89%E7%94%A8%201%201.%E7%B0%A1%E5%96%AE%E8%AA%8D%E8%AD%98CSS%20grid%20%E7%B6%B2%E6%A0%BC%E7%B3%BB%E7%B5%B1%20grid%E6%98%AFcss%E4%B8%AD%E5%A5%BD%E7%94%A8%E7%9A%84%E6%8E%92%E7%89%88%E6%96%B9%E5%BC%8F%EF%BC%8C%E9%80%8F%E9%81%8E%E8%A8%AD%E5%AE%9A%E6%AC%84%EF%BC%88column%29%E5%88%97%20%28row%29%E4%BE%86%E9%81%94%E6%88%90%E5%83%8Fexcel%E9%82%A3%E6%A8%A3%E7%9A%84%E7%B6%B2%E6%A0%BC%E6%8E%92%E7%89%88%E3%80%82,%E5%B8%83%E7%BD%AE%E5%A5%BD%E5%85%A7%E5%AE%B9%E5%BE%8C%EF%BC%8C%E5%B0%B1%E8%A9%B2%E8%AA%BF%E6%95%B4%E7%B4%B0%E9%83%A8%E5%95%A6%21%20grid%E4%B8%80%E6%A8%A3%E4%B9%9F%E6%9C%89%E8%AA%BF%E6%95%B4%E9%96%93%E9%9A%94%E7%9A%84%E5%B1%AC%E6%80%A7%EF%BC%8C%E4%BB%A5%E5%8F%8A%E8%87%AA%E8%BA%AB%E5%B0%8D%E9%BD%8A%E8%88%87%E6%95%B4%E9%AB%94%E5%B0%8D%E9%BD%8A%E7%9A%84%E8%A8%AD%E5%AE%9A%E5%96%94%21%20...%204%205.%E7%AF%84%E4%BE%8B%26grid%E5%B0%8F%E9%81%8A%E6%88%B2%20%E9%80%99%E9%82%8A%E6%8E%A8%E8%96%A6%E4%B8%80%E5%80%8B%E9%97%9C%E6%96%BCcss%20grid%E7%9A%84%E5%B0%8F%E9%81%8A%E6%88%B2%EF%BC%8C%E9%80%8F%E9%81%8E%E8%A8%AD%E5%AE%9A%E6%A0%BC%E7%B7%9A%E4%BE%86%E6%BE%86%E8%8A%B1%E5%92%8C%E9%99%A4%E8%8D%89%EF%BC%8C%E6%9C%83%E5%B8%B6%E4%BD%A0%E4%B8%80%E6%AD%A5%E4%B8%80%E6%AD%A5%E4%BA%86%E8%A7%A3grid%E7%9A%84%E7%94%A8%E6%B3%95%E3%80%82%20)學的。  
想練習的話，文章作者有寫一個[範例](https://codepen.io/yukiyin/pen/abqweRL)，你可以在裡面調整代碼看看有甚麼變化。  
這裡還有一個她推薦練習`grid布局`的[小遊戲](https://cssgridgarden.com/)。



## JavaScript的部分
接下來就是`JavaScript`的部分，我一樣依照順序講解。

### 時間功能
我先做畫面左上角的`時間`。  
  
首先，我們要獲取`HTML`中的`時`和`分`元素。

```javascript
// DOM Elements
const hourEl=document.querySelector('.hour');
const minuteEl=document.querySelector('.minute');
```

接下來寫一個`updateTime`的功能。

```javascript
// Set up the time
const updateTime=()=>{
    const currentTime=new Date(); // 初始化日期

    let currentHour=currentTime.getHours(); // 抓現在幾時
    const currentMinute=currentTime.getMinutes(); // 抓現在幾分

    if(currentHour>12){    // 表達成12小時進制
        currentHour-=12;
    }
    hourEl.textContent=currentHour.toString(); // 把原本的小時用新的替換掉
    minuteEl.textContent=currentMinute.toString().padStart(2,'0'); // 把原本的分鐘用新的替換掉，並自動補齊兩位數
}
```

最後不要忘記，讓它每秒重新跑一次。

```javascript
// Set up the time
setInterval(updateTime, 1000);
```

一開始也要記得呼叫它出來。

```javascript
// Set up the time
updateTime();
```

這樣`時間`的部分就大功告成了。

### 計算器功能
接下來來做`計算器`的功能。  
  
一樣的，我們先獲取每個`按鍵`的元素。

```javascript
// DOM Elements
const acEl=document.querySelector('.ac');
const pmEl=document.querySelector('.pm');
const percentEl=document.querySelector('.percent');

const additionEl=document.querySelector('.addition');
const subtractionEl=document.querySelector('.subtraction');
const multiplicationEl=document.querySelector('.multiplication');
const divisionEl=document.querySelector('.division');
const equalEl=document.querySelector('.equal');

const decimalEl=document.querySelector('.decimal');
const number0El=document.querySelector('.number-0');
const number1El=document.querySelector('.number-1');
const number2El=document.querySelector('.number-2');
const number3El=document.querySelector('.number-3');
const number4El=document.querySelector('.number-4');
const number5El=document.querySelector('.number-5');
const number6El=document.querySelector('.number-6');
const number7El=document.querySelector('.number-7');
const number8El=document.querySelector('.number-8');
const number9El=document.querySelector('.number-9');
```

來造一個`陣列`把我們每個`number按鍵`放進去，這樣的話在等等後續操作處理會方便一些。

```javascript
// DOM Elements
const numberElArray=[
    number0El, number1El, number2El, number3El, number4El,
    number5El, number6El, number7El, number8El, number9El
];
```

我們接著先把大致架構寫出來。  
第一步，第一個事件就是接收`數字按鈕點擊`。

```javascript
// Add Event Listeners to numbers and decimal
for(let i=0;i<numberElArray.length;i++){
    const numberEl=numberElArray[i];
    numberEl.addEventListener('click',()=>{  // 這就是為何把number按鍵塞進陣列的原因，在Listen時就不需要一個個寫出來
        handleNumberClick(i.toString()); // 把點擊的按鈕代表的數值丟去處理
    });
}
```

第二步，來寫`數字按鈕點擊的處理`。

```javascript
// Functions
const getValueAsStr=()=>valueEl.textContent.split(',').join('');  // 要讓字符串每三個位數就用逗號分隔，split分割，join把數組中的所有元素放入一個字符串。元素是通過指定的分隔符進行分隔的。

const handleNumberClick=(numStr)=>{
    const currentValueStr=getValueAsStr();
    if(currentValueStr==='0'){  //因為它是一個個字串，我們在這判斷是否輸入過別的數，有就把這幾個字串接起來
        setStrAsValue(numStr);  //這功能細節等等再回來說
    } 
    else{
        setStrAsValue(currentValueStr+numStr);
    }
};
```

我們回過頭來處理`十進制與小數點`的部分。

```javascript
// Add Event Listeners to numbers and decimal
decimalEl.addEventListener('click',()=>{
    const currentValueStr=getValueAsStr();
    if(!currentValueStr.includes('.')){  // 之前沒有小數點的話那就給它一個
        setStrAsValue(currentValueStr+'.');
    }
});
```

處理好後，我們把前面提到的`setStrAsValue`的細節寫完。

```javascript
// Functions
const setStrAsValue=(valueStr)=>{
    if(valueStr[valueStr.length-1]==='.'){  // 你要小數點那就給你加上吧
        valueEl.textContent+='.';
        return;
    }

    const[wholeNumStr,decimalStr]=valueStr.split('.');  // 處理浮點數，這邊非常直觀
    if(decimalStr){
        valueEl.textContent=parseFloat(wholeNumStr).toLocaleString()+'.'+decimalStr; 
    } 
    else{
        valueEl.textContent=parseFloat(wholeNumStr).toLocaleString(); // toLocaleString讓字符串每三位用逗號分隔
    }
};
```

之後的步驟就非常簡單了。  
第三步，處理完`number按鍵`那就先來處理`function按鍵`吧。

```javascript
// Add Event Listeners to functions
acEl.addEventListener('click',()=>{  // 歸零鍵
    setStrAsValue('0');
    valueStrInMemory=null;  // 暫存的值
    operatorInMemory=null;  // 暫存的運算子
});

pmEl.addEventListener('click',()=>{  // 正負號
    const currentValueNum=getValueAsNum();  // 畫面上的數值
    const currentValueStr=getValueAsStr();

    if(currentValueStr==='-0'){
        setStrAsValue('0');
        return;
    }
    if(currentValueNum >= 0){
        setStrAsValue('-'+currentValueStr);
    } 
    else{
        setStrAsValue(currentValueStr.substring(1));  // 去掉第一個元素，簡單來說就是把負號拔掉
    }
});

percentEl.addEventListener('click',()=>{  // 百分比
    const currentValueNum=getValueAsNum();
    const newValueNum=currentValueNum/100;
    setStrAsValue(newValueNum.toString());
    valueStrInMemory=null;
    operatorInMemory=null;
});
```

不要忘記把`變量`補上去。

```javascript
// variables
let valueStrInMemory=null;
let operatorInMemory=null;
```

也不要忘記把`getValueAsNum`補上去。

```javascript
// Functions
const getValueAsNum=()=>{
    return parseFloat(getValueAsStr());
};
```

第四步，處理完`function按鍵`那就再來處理`operator按鍵`吧。

```javascript
// Add event listeners to operators
additionEl.addEventListener('click',()=>{  // 加
    handleOperatorClick('addition');
});
subtractionEl.addEventListener('click',()=>{  // 減
    handleOperatorClick('subtraction');
});
multiplicationEl.addEventListener('click',()=>{  // 乘
    handleOperatorClick('multiplication');
});
divisionEl.addEventListener('click',()=>{  // 除
    handleOperatorClick('division');
});
equalEl.addEventListener('click',()=>{  // 等於
    if(valueStrInMemory){
        setStrAsValue(getResultOfOperationAsStr());  // getResultOfOperationAsStr也就是運算，等等最後來做
        valueStrInMemory=null;
        operatorInMemory=null;
    }
});
```

第五步，就像`數字按鈕點擊的處理`一樣，來寫一下`運算子按鈕點擊的處理`。

```javascript
// Functions
const handleOperatorClick=(operation)=>{
    const currentValueStr=getValueAsStr();

    if(!valueStrInMemory){  // 暫存的值是空的話
        valueStrInMemory=currentValueStr;
        operatorInMemory=operation;
        setStrAsValue('0');
        return;
    }
    valueStrInMemory=getResultOfOperationAsStr();  // 最後一步
    operatorInMemory=operation;
    setStrAsValue('0');
};
```

終於，最後一步，我叫你`算`。

```javascript
const getResultOfOperationAsStr=()=>{
    const currentValueNum=getValueAsNum();
    const valueNumInMemory=parseFloat(valueStrInMemory);
    let newValueNum;
    if(operatorInMemory==='addition'){  // 加
        newValueNum=valueNumInMemory+currentValueNum;
    } 
    else if(operatorInMemory==='subtraction'){  // 減
        newValueNum=valueNumInMemory-currentValueNum;
    } 
    else if(operatorInMemory==='multiplication'){  // 乘
        newValueNum=valueNumInMemory*currentValueNum;
    } 
    else if(operatorInMemory==='division'){  // 除
        newValueNum=valueNumInMemory/currentValueNum;
    }

    return newValueNum.toString();
};
```

好了，具體上來說大概就這樣，有問題就問學長姐吧，我應該答不出來。