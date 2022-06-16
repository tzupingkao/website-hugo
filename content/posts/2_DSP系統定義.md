---
title: "2_DSP系統定義"
date: 2022-06-16T11:14:08+08:00
categories:
- Signal_Processing
- DSP Class
tags:
- signal_processing
thumbnailImagePosition: left
thumbnailImage: //d1u9biwaxjngwg.cloudfront.net/chinese-test-post/vintage-140.jpg
mathjax: true
---

解釋 DSP 系統定義與類型中訊號的數學表示法
<!--more-->

# 2. DSP系統定義

DSP系統

> 若輸入的數位訊號為 $x \lbrack n \rbrack$，輸出的數位訊號為 $ y\lbrack n \rbrack$，
> 則 DSP 系統可以數學表達
> $$y\lbrack n\rbrack=T\{x\lbrack n\rbrack\}$$
> 其中，$T\{\cdot\}$就是DSP系統，或稱為系統的 Transform
> 

## 2.1 動態與靜態系統

動態系統

> 動態系統 (Dynamic System)是指輸出訊號 $y\lbrack n\rbrack$ 的計算包含**過去**、**現在**與**未來**的數位訊號，也稱作記憶系統 (Memory System)
> 

靜態系統

> 靜態系統 (Static System)是指輸出訊號 $y\lbrack n\rbrack$ 的計算是根據目前的輸入 $x\lbrack n\rbrack$ 而得，也稱作無記憶系統 (Memoryless System)
> 

**動態**與**靜態**系統分別被稱為**記憶**系統與**無記憶**系統

(根據是否需要額外記憶體紀錄過去資料用於計算)

## 2.2 因果系統

> 因果系統 (Causal System)是指DSP的輸出 $y\lbrack n\rbrack$ ，僅根據**目前**與**過去**的輸入訊號運算而得
> 
- Causal這個詞如果在Google翻譯是 "因果關係”，但是我一開始聽到的時候覺得很詭異。
- 可以這樣理解，因為系統的輸出只跟**目前**與**過去**的訊號有關，不牽扯到未來
因此是根據**目前**與**過去**的訊號這個 "因”，導致系統輸出這個 “果"，而得名。
- 或者說可以這樣想，”因果關係” 中的 “因" 不大可能是發生在未來 (生活中應該是這樣的經驗吧?)，所以 因果系統 就是專指過去與現在的訊號所產生的輸出
- 因果系統聽起來很理所當然，非因果系統怎麼可能出現呢?? 數學上是會出現的，後續做濾波器設計的地方會出現。

## 2.3 線性系統

> 線性系統 (Linear System)是指DSP系統符合線性原則
即: $$T\{\alpha\cdot x_1\lbrack n\rbrack+\beta\cdot x_2\lbrack n\rbrack\}=\alpha\cdot T\{x_1\lbrack n\rbrack\}+\beta\cdot T\{x_2\lbrack n\rbrack\}$$
> 

## 2.4 非時變系統

> 非時變系統 (Time-Invariant System)是指DSP系統的運作，不會隨著時間而改變
即: $$y\lbrack n\rbrack=T\{x\lbrack n\rbrack\}$$
若時間延遲 $n_0$
則: $$y\lbrack n-n_0\rbrack=T\{x\lbrack n-n_0\rbrack\}$$
> 

上述的線性系統與非時變系統，簡稱**線性非時變** (Linear Time-Invariant, LTI)系統
是貫穿整個DSP理論的系統，基本上後續的傅立葉轉換、頻譜分析、濾波器設計等等議題
都是基於LTI的性質做出數學推導，請大家記住這個性質

## 2.5 系統穩定性

穩定系統

> 穩定系統 (Stable System):
> 是指系統有限輸入-有限輸出 (Bounded Input-Bounded Output, BIBO)。
>
> DSP系統: $y\lbrack n\rbrack=T\{x\lbrack n\rbrack\}$
>
> 若 $$\left|x\lbrack n\rbrack\right|<B_x<\infty\;,\;-\infty<n<\infty$$
> 則 $$\left|y\lbrack n\rbrack\right|<B_y<\infty\;,\;-\infty<n<\infty$$
> 稱此DSP系統BIBO穩定
> 

也就是說當系統輸入訊號落在限定範圍，輸出訊號也會落在限定範圍，就稱為BIBO穩定系統。

穩定系統範例

> DSP系統: 
> $$y\lbrack n\rbrack=\frac13(x\lbrack n\rbrack+x\lbrack n-1\rbrack+x\lbrack n-2\rbrack)$$
> 假設 $$\left|x\lbrack n\rbrack\right|<B_x<\infty\;,\;-\infty<n<\infty$$
> 判斷系統穩定性
> 

解法

> $
> \begin{aligned}
> \left|y\lbrack n\rbrack\right| 
> & = \left|\frac13(x\lbrack n\rbrack+x\lbrack n-1\rbrack+x\lbrack n-2\rbrack)\right|\\\
> & \leq\frac13(\left|x\lbrack n\rbrack\right|+\left|x\lbrack n-1\rbrack\right|+\left|x\lbrack n-2\rbrack\right|)\\\
> & \leq\frac13(B_x+B_x+B_x)=B_x<\infty
> \end{aligned}
> $
> 此系統為BIBO穩定
> 

非穩定系統範例

> DSP系統: 
> $$y\lbrack n\rbrack=r^n\cdot x\lbrack n\rbrack\\;,\\;r>1$$
> 假設 $$\left|x\lbrack n\rbrack\right|<B_x<\infty\;,\;-\infty<n<\infty$$
> 判斷系統穩定性
> 

解法

> $
> \begin{aligned}
> \left|y\lbrack n\rbrack\right| & = \left|r^n\cdot x\lbrack n\rbrack\right|\\\
> & = \left|r^n\right|\cdot\left|x\lbrack n\rbrack\right|\xrightarrow{n\rightarrow\infty}\infty
> \end{aligned}
> $
> 此系統BIBO**不**穩定
>