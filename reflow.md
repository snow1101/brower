
# 有关重绘或者重排的小常识

* 浏览器会缓存一些变化，然后在一个时间内一起进行重绘和重排

```
var $body = $('body');
$body.css('padding', '1px'); // reflow, repaint
$body.css('color', 'red'); // repaint
$body.css('margin', '2px'); // reflow, repaint
// only 1 reflow and repaint will actually happen

```
* 但是，通过获取元素的一些属性会引起强制的重排，所以在一些场景下（比如 移除了一个动画class，之后将div的margin改变，继续加上此动画class，可能效果并非预期，就是因为浏览器缓存了这些动画，执行了一次重排，所以若需强制重排，可通过获取offsetHeight等元素引起强制重排）

```
var $body = $('body');
$body.css('padding', '1px');
$body.css('padding'); // reading a property, a forced reflow
$body.css('color', 'red');
$body.css('margin', '2px');
```
* 修改一个绝对定位的元素，只会引起这个元素及其子元素的重排，修改文档流元素的一个属性，会影响整个文档流的重排，所以动画的元素尽量放到绝对定位的元素中
