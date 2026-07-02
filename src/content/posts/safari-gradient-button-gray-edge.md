---
title: "Safari 圓形漸層鈕的「灰邊」問題"
author: dbb
pubDatetime: 2026-07-02T17:28:20.000+08:00
modDatetime:
featured: false
tags:
  - css
description: "一顆黑色圓鈕 hover 變漸層色，一個很常見的設計，在 Chrome / Firefox 正常，但在 Safari 的時候，圓的最外圈會多一圈灰髒髒的邊。"
---

## 一、問題的來源

> [!info]
> 一顆黑色圓鈕 hover 變漸層色，一個很常見的設計，在 Chrome / Firefox 正常，但在 Safari 的時候，圓的最外圈會多一圈灰色的邊。

這個其實在之前就有遇到過幾次，但是很多時候公司都會默認很少人用 Safari ，所以都可以混水摸魚過去，不用處理。但這次剛好遇到一個熱愛使用 Safari 的設計師。她對於這個灰邊非常的介意，甚至把這個列為上線前必須修好的程度。也就是因為這樣，所以我只好來研究怎麼做了。

---

## 二、解決方案

當然這件事其實交給 AI 處理非常快，剛好遇到今天 Fable 5 解禁，我想說就都來簡單的測試看看，到底它們會用什麼方法來解決問題。

我用了 Codex 5.5 、 Opus 4.8 、 Fable 5 三個不同的模型來處理，都用一樣的 prompt ，就是上面 Info 的內容。

結果它們分別給出不同的解法：

- Codex 與 Opus：hover 後把漸層層稍微放大，用覆蓋的方式蓋住灰邊。
- Fable：把底層背景色換成漸層的中間色，讓邊緣即使有滲色也不明顯。

實際測起來，Fable 給的效果比較好。不過這裡不是要說哪個模型比較強，而是這兩種方法其實都讓我意識到，我之前對這個問題的理解不夠深。我以前就只會很粗暴的把背景設定為透明，然後希望背景色跟漸層色顏色不要差距太大，就不會被發現了。

不過又遇到了，感覺還是需要來理解一下為什麼會發生，然後這些解法是解決了什麼問題，不然這就只是一篇吹捧 AI 的文章而已。

## 三、問題的原因

我覺得最重要的概念是，一個元素的背景其實是有多層的。例如我們很常寫：

```css
.button {
  background-color: #000;
  background-image: linear-gradient(135deg, #ffd84d, #4ade80);
}
```

可以把它想成：

- 上層：background-image → 漸層色
- 下層：background-color → 黑色底

上層的漸層會蓋住下層的黑色背景。理論上應該只會看到漸層，看不到黑色底。但問題就出在「圓形邊緣」上。螢幕是由一格一格的方形像素組成的，但圓形邊緣是弧線。為了讓弧線看起來平滑，瀏覽器會在邊緣做反鋸齒處理，也就是用一些半透明像素來柔化邊界。

在這個案例中， Safari / WebKit 的結果看起來就像是：它在處理同一個元素裡的不同背景層時，邊緣裁切與反鋸齒的計算的方式不一樣。

- 黑色底:切到圓的正常邊緣。
- 上層:看起來切得比圓的邊緣往內縮了不到一個像素，這可能要去看實作方式才知道到底真的差距多少。

雖然差距不到一個像素，但是邊緣就會有底色的滲透，加上這次使用的是比較明亮的漸層色，底下的灰色像素就變得格外明顯。

---

## 四、解決方法的差異

我目前理解的有三種，如果有更多的歡迎再跟我講。

---

### 背景設置為透明

這是我以前最直覺的解法。

```css
.button:hover {
  background-color: transparent;
  background-image: linear-gradient(135deg, #ffd84d, #4ade80);
}
```

這個解法的邏輯是：既然問題是黑色底從邊緣透出來，那就把黑色底變透明。

但是如果背景有顏色的話，例如圖片或是卡片，一樣會有不自然的鋸齒或是雜色。所以只適合剛好在某些背景下有效果。

### 把漸層放大

第二種做法是讓漸層比原本的圓形大一點，直接把邊緣可能露出的底色蓋住。

```css
.button::before {
  content: "";
  position: absolute;
  inset: -1px;
  border-radius: inherit;
  background-image: linear-gradient(135deg, #ffd84d, #4ade80);
  opacity: 0;
  transition: opacity 0.2s ease;
}
```

程式碼太長了，就不全部貼上來了，重點就是 `inset: -1px;`這段。

這個解法的邏輯是：這樣即使 Safari 在計算漸層邊緣時會往內縮，也還有多出來的漸層可以補上。

不過缺點就是很明顯，按鈕在 Hover 的時候會變大，不過這也可以說是一種設計就是了。

### 設置中間色

第三種方法是我這次覺得最合理的做法：不要把底色設成黑色，而是在 hover 時把底色改成接近漸層的中間色，而且 css 也短很多。

```css
.button:hover {
  background-color: #9ee76a;
  background-image: linear-gradient(135deg, #ffd84d, #4ade80);
}
```

這個做法的邏輯是：讓背景顏色就算滲出來，也看不出來。

因為問題的本質是，下層背景會從邊緣露出來，所以把下層背景換成接近上層漸層的顏色。這樣即使邊緣有半個像素的誤差，露出來的也不是黑色，而是和漸層相近的顏色。視覺上就不會出現明顯的灰邊。

這個做法的好處是非常簡單，要說有什麼缺點的話，大概就是漸層色如果差距太大，就算是填充中間色也會看起來很奇怪。

---

## 五、延伸閱讀

- [CSS: Fixing background color bleed in rounded corners (DEV.to)](https://dev.to/rashidshamloo/css-fixing-background-color-bleed-in-rounded-corners-2kh4) - 也是遇到類似的問題，重點在於找出洩漏出來的是哪一層，然後再來解決。

- [Fixing the Safari background 'bleed' (19eighty7)](https://19eighty7.com/post/937368654/fixing-the-safari-background-bleed) - 比較沒幫助，這是討論另一問題，背景色滲透到 border 的問題。

- [Mozilla bug 921341](https://bugzilla.mozilla.org/show_bug.cgi?id=921341) — 雖然是 Firefox table cell 的案例，但裡面討論到 rounded corner 下，不同背景繪製路徑應該使用一致的 border-radius，和這篇的問題很相似。
