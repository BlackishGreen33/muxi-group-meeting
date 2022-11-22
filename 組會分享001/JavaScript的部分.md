# JavaScript的部分
接下來就是`JavaScript`的部分，我一樣依照順序講解。

## 時間功能
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

## 計算器功能
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