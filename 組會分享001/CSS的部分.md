# CSS的部分
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

## grid網格布局
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