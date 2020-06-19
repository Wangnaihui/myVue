# my-vue参照vue.js实现双向数据绑定

实现了

通过v-model和{{}}来双向绑定数据

利用v-on绑定给元素节点绑定事件并添加MyVue实例methods中相应的方法

整体采用数据劫持结合发布订阅模式，通过Object.defineProperty()来劫持各个属性的getter,setter, 在数据变动时发布消息给订阅者，触发相应的回调函数，从而实现数据双向绑定。



构造函数：

​				MyVue负责创建初始化实例对象。

​				Observer负责创建监听器，实现对MyVue.data对象数据的层层监听并为其中每个属性创建相应的订阅器（Dep）。

​				Dep负责创建订阅器实例，存储与其对应的属性的所有订阅者，实现添加订阅者与通知订阅者的功能。

​				Compile负责对文档流的控制，对元素节点和文本节点进行操作，匹配“v-”属性添加相应事件或绑定相应数据，并初始化视图，在v-model和{{}}处创建新				的订阅者。

​				Watcher负责创建订阅者实例，并将自己添加到相应的属性订阅器中，在收到订阅器更新通知时触发回调函数更新视图数据。



注：订阅者有两种：一种是v-model创建的订阅者，另一种是{{}}创建的订阅者，他们的回调函数略有不同



