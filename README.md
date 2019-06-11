# react
# react从诞生之初就是可以被逐步采用的，因而你可以按需引入react特性。
ReactDom.render(
<h1>hello,world!</h1>,
doucument.getElementById('root')
);
# react应用程序的组成部分：元素和组件（可以使用这些可以复用的小片段组成复杂的应用）
# react是一个javascript库
# jsx简介
const element = <h1>hello,world!</h1>;
这个被称为jsx，是javascript的语法扩展，他可以很好描述ui应该呈现出它应有交互的本质形式。
jsx可能会使人联想到模板语言。jsx可以生成react元素
为什么使用jsx，react认为渲染本质上和其他ui逻辑内在耦合，在ui中需要绑定事件，在某些时刻状态发生
的变化需要通知到ui，以及需要在ui中展示准备好的数据。
react没有采用将标记与逻辑分离到不同的文件中这种人为的分离，而是通过将二者共同存放在称之为
‘组件’的松散耦合中，来实现关注点分离
react不强制要求使用jsx
在jsx中嵌入表达式
我们声明了一个名为name的变量，让后在jsx中使用它，并将他包裹在大括号中：
const name='josh peter'
const element = <h1>hello{name}</h1>
ReactDom.render(
element,
document.getElementById('root')
);
在jsx语法中，你可以在大括号内放任何有效的javascript表达式
下面实例中我们将调用javascript函数的结果，并且嵌入到<h1>元素中
function formatName(user) {
  return user.firstName + '' +user.lastName;
}
const user = {
  firstName: 'add',
  lastName： 'jack'
};
const elemet = {
  <h1>
  hello,{formatName}
  </h1>
};
ReactDom.render(
  element,
  doucument.getElementById('root')
);
# jsx也是一个表达式，在编译之后jsx表达式会被转化成普通的javascript函数调用，并且取值后得到javascript对象
也就是说，你可以在if和for循环的代码块中使用jsx，将jsx赋值给变量，把jsx当作参数传入，以及从函数中返回jsx
function getGreeting(user) {
 if(user) {
   reutrn <h1>hello{formatName(user)}</h1>
 }
 jsx特定属性
 你可以通过使用引号，来将属性值指定为字符串字面量
 const element = <div tabIndex="0"></div>
 也可以使用大括号，赖在属性值中插入一个javascript表达式：
 const element = <img src={user.avatarUrl}></img>
 因为jsx在语法上更接近javascript而不是html，所以react使用小驼峰命名来定义属性的名称，而不使用html属性名称命名属性
 ！jsx里的class变成了className，tabindex变成tabIndex
 使用jsx指定子元素，假定一个标签里没有内容，可以用/来闭合，（类似xml语法）
 const element = <img src={user.avatarUrl}/>;
 !jsx标签里能够包含很多子元素
 const element = {
  <div>
  <h1>hello!
  </h1>
  </div>
 }
 jsx防止注入攻击
 !你可以安全的在jsx中插入用户输入内容
 const title = response.potentaillyMaliciousInput;
 const element = <h1>{title}</h1>
 react在渲染所有输入内容之前，默认进行转义。（可以确保在应用中，永远不会注入一些非自己明确编写的内容
 所有的内容都在渲染之前被转换成字符串，这样可以防止xss（跨站脚本攻击））？
 jsx表示对象
 babel会把jsx转翻译陈一个名为React.createElement()函数调用
 以下两种代码完全等效：
 const element = {
   <h1 className="geeeting">
   hello!world
   </h1>
 }
 const element = React.createElement(
 'h1',
 {className: 'geeeting'},
 'hello!world'
 react会预先执行一些检查，来帮你编写无错代码，但他实际创建了这样一个对象
 const element = {
 type: 'h1',
 props: {
   className: 'geeting',
   children: 'hello!world'
 }
 }
 );
 这些对象被称为react元素，react通过读取这些对象，然后使用它们来重构dom保持更新
 # 元素渲染
 元素是构成react应用大的最小砖块
 const element = <h1>hello!world</h1>
 与浏览器dom不同，react元素是创建开销极小的普通对象
 将一个元素渲染为dom
 假设你的html文件有一个<div>
 <div id="root"></div>
 我们把他称为根dom节点，里面所有的内容都归reactdom管理
 仅仅使用react构建的应用通常只有单一的根dom节点
 但是如果在一个已有的应用中敖汉任意多的独立dom节点
 !想要将一个react元素渲染到根dom节点中，只需要把它们一起传入reactDom.render()
 const element = <h1>hello!world</h1>;
 ReactDom.render(element,document.getElementById('root'))
 更新已经渲染的元素
 ！react元素是不可变对象，一旦被创建，就无法更改它的子元素或属性。一个元素就像电影的单帧：表示某个特定时候的ui
 更具我们已经有的知识，更新ui的唯一的方式是创建一个全新的元素，并将其传入ReactDom.render()
 一个计时器：
 function tick() {
   const element = (
   <div>
     <h1>
     it is {new Date().toLocaleTimeString()}
     </h1>
   </div>
   );
   ReactDom.render(element, doucment)
 }
