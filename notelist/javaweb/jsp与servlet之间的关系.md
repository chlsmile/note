## jsp与servlet之间的关系

#### jsp的本质
- jsp在首次被访问的时候被应用服务器转换为servlet，在以后的运行中，容器直接调用这个servlet，而不再访问jsp页面。jsp的实质仍然是servlet。

#### jsp的作用
- java服务器页面(JSP)是HttpServlet的扩展.由于HttpServlet大多是用来响应HTTP请求,并返回Web页面(例如HTML、XML),所以不可避免地,在编写servlet时会涉及大量的HTML内容,这给servlet的书写效率和可读性带来很大障碍,JSP便是在这个基础上产生的.其功能是使用HTML的书写格式,在适当的地方加入Java代码片段,将程序员从复杂的HTML中解放出来,更专注于servlet本身的内容。