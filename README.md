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