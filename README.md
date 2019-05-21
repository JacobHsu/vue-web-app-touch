# vue-web-app

`vue init webpack left-delete`  n n n 

`$ cd left-delete`
`$ npm run dev`

# left-delete

每個觸控事件被觸發後，會生成一個event對象，event對象裡額外包括以下觸控列表  

`touches`: 當前屏幕上所有手指的列表  
`changedTouches`: 涉及當前事件的手指的列表，儘量使用這個代替touches 

這些列表裡的每次觸控由touch對象組成，touch對象裡包含著觸控信息，主要屬性如下：

`clientX / clientY:` 觸摸點相對瀏覽器窗口的位置  

當滑塊沒有超過刪除按鈕的一半時自動回到起點位置。點擊刪除後調用deleteLine刪除當前行

# References

[使用Vue实现移动端左滑删除效果](https://www.helloweba.net/javascript/607.html)  