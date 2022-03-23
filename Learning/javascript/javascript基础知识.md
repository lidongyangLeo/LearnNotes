## 事件

事件流描述的是从页面中接收事件的顺序。

IE 的事件流是事件冒泡

而Netscape Communicator 的事件流式事件捕获流。

### 事件冒泡

- IE 的事件流叫做事件冒泡，即事件开始时由最具体的元素接收，然后逐级向上传播到较为不具体的节点。

  ``` html
  <!DOCTYPE html>
  <html>
  <head>
      <title>Event Bubbling Example</title>
  </head>
  <body>
      <div id="myDiv">Click Me</div>
  </body>
  </html>
  ```

  如果你单击了页面中的<div>元素，那么这个click事件会按照如下顺序传播：

  1. div
  2. body
  3. html
  4. document

  所有现代浏览器都支持事件冒泡。

  

  ### 事件捕获

  Netscape Communicator 团队提出了另一种事件流叫做事件捕获。事件捕获的思想是不太具体的节点应该更早接收到事件，而最具体的节点应该最后接收到事件。

  1. document

  2. <html>

  3. <body>

  4. <div>
       <div>

  5. 在事件捕获过程中，docuemnt对象首先接收到click事件，然后事件沿DOM树依次向下，一直传播到事件的实际目标。

     由于老版本的浏览器不支持，因此很少有人使用事件捕获。我们也建议使用事件冒泡。

  ### DOM 事件流

  DOM2级事件 规定的事件流包括三个阶段： 

  - 事件捕获阶段
  - 处于目标阶段
  - 事件冒泡阶段

  

