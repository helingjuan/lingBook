# Vue相关面试题
<!-- TOC -->

- [Vue相关面试题](#vue相关面试题)
  - [说说对MVVM的理解](#说说对mvvm的理解)
    - [说说MVC，MVP，MVVM三种组合模式分别有怎么样的理解？](#说说mvcmvpmvvm三种组合模式分别有怎么样的理解)
  - [vue的优点是什么？](#vue的优点是什么)
  - [你知道Vue响应式数据原理吗？2.0和3.0的有什么区别？](#你知道vue响应式数据原理吗20和30的有什么区别)
    - [vue数据双向绑定的原理](#vue数据双向绑定的原理)
      - [深度理解](#深度理解)
    - [vue3.0的响应式原理](#vue30的响应式原理)
      - [Proxy只会代理对象的第一层，vue3.0如何解决？](#proxy只会代理对象的第一层vue30如何解决)
      - [监听数组的时候可能触发多次get/set,那么如何防止触发多次呢？](#监听数组的时候可能触发多次getset那么如何防止触发多次呢)
    - [Proxy和Object.defineProperty的区别](#proxy和objectdefineproperty的区别)
  - [vue2.0 组件通信有哪些方式？:question:](#vue20-组件通信有哪些方式)
  - [v-if和v-show 有什么区别？](#v-if和v-show-有什么区别)
  - [computed和watch的区别和运用的场景？](#computed和watch的区别和运用的场景)
  - [组件中的data为什么是一个函数？](#组件中的data为什么是一个函数)
  - [v-model是如何实现双向数据绑定的？](#v-model是如何实现双向数据绑定的)
  - [nextTick的实现原理是什么？](#nexttick的实现原理是什么)
  - [Vue事件绑定原理是什么？](#vue事件绑定原理是什么)
  - [为什么不建议用index作为key？](#为什么不建议用index作为key)
  - [Vue中组件的生命周期调用顺序是怎么样的？](#vue中组件的生命周期调用顺序是怎么样的)
  - [在什么阶段才能访问操作DOM？](#在什么阶段才能访问操作dom)
  - [接口请求一般放在哪个生命周期中？](#接口请求一般放在哪个生命周期中)
  - [vue路由有几种模式？他们的实现原理分别是什么？区别在哪？](#vue路由有几种模式他们的实现原理分别是什么区别在哪)
    - [hash和history的区别？](#hash和history的区别)
  - [路由懒加载是什么意思？如何实现路由懒加载？](#路由懒加载是什么意思如何实现路由懒加载)
  - [vue Router导航守卫有哪些？](#vue-router导航守卫有哪些)
  - [vuex是什么？](#vuex是什么)
    - [vuex的组成](#vuex的组成)
    - [什么情况下使用vuex？](#什么情况下使用vuex)
    - [vuex和全局对象有什么区别？](#vuex和全局对象有什么区别)
    - [为什么vuex的mutation中不能做异步操作？](#为什么vuex的mutation中不能做异步操作)
      - [为什么可以跟踪每个状态的变化？](#为什么可以跟踪每个状态的变化)
  - [说说vue和react的异同？](#说说vue和react的异同)
  - [什么是mixin（混入）？](#什么是mixin混入)
  - [vue模板编译原理知道吗？简单描述一下](#vue模板编译原理知道吗简单描述一下)
  - [diff算法说一下](#diff算法说一下)
  - [说一说对keep-alive的理解](#说一说对keep-alive的理解)
  - [说说对SSR的了解](#说说对ssr的了解)
  - [对vue3.0的特性你有什么了解？](#对vue30的特性你有什么了解)
- [参考资料](#参考资料)

<!-- /TOC -->

## 说说对MVVM的理解
Model View viewModel 的缩写，model代表数据模型，view代表UI组件，viewModel监听模型数据的改变和控制视图的行为，处理用户交互,也就是把数据模型和UI组件关联起来，实现数据双向绑定
这样开发者就可以只要关注业务逻辑，不用手动操作DOM，也不用处理数据状态了，数据状态统一由MVVM进行管理
### 说说MVC，MVP，MVVM三种组合模式分别有怎么样的理解？
UI和逻辑分化后带来的实质问题：**是按逻辑和UI划分地管理，还是按单界面的事务进行划分地管理**
MVC、MVP和MVVM本质上都是源于职能划分和规划的思想与目的
- MVC（Model-View-Controller）
  Model 代表数据，View代表界面，Controller处理业务，view向Controller触发事件，controller作出相应处理，并把数据反馈给Model和View。而model层如果有数据发生变化，会通知Controller层。从而二次更新。
  缺点：1. 没有明确的定义，所以不同的实现细节上都是不一样的。
        2. 在有变化的时候，需要同时维护3个对象和3个交互，让事件复杂化了。
- MVP（Model-View-Presenter）
  对MVC的改进点：切断view和Model的联系，让View只和Presenter(原Controller)交互，减少在需求变化中需要维护的对象的数量
- MVVM（Model-View-ViewModel）
  通过数据双向绑定，简化了业务和界面的依赖关系，优化了数据频繁更新的解决方案

## vue的优点是什么？
- 低耦合
- 可重用性
- 独立开发
- 可测试
## 你知道Vue响应式数据原理吗？2.0和3.0的有什么区别？
### vue数据双向绑定的原理
表现就是：数据变化更新视图，视图变化更新数据。其中View变化更新data，可以通过事件监听的方式来实现，所以主要是处理**如何根据data变化更新view**
这个就是主要通过**Object.defineProperty()**这个方法。vue遍历data里的所有擦拿书，并使用**Object.defineProperty()**把这些参数全部转为getter/setter,这些getter/setter对用户来说是不可见的，但是在内部它们让vue能够追踪依赖，在property被访问和修改时通知变更。

每个组件实例都对于一个watcher实例，它会在组件渲染的过程中把接触过的数据property记录为依赖，当依赖项的setter触发时，会通知watcher，从而使它关联的组件重新渲染。

> Object.defineProperty()有什么缺陷吗？
> 对数组和对象的监听有问题，需要深度监听才能实现真正地监听

#### 深度理解
**监听器Observe**：对数据对象进行遍历，利用**Object.defineProperty()**对数据对象及其属性加上getter/setter。这样，如果给对象的某个值复制，就会触发setter，从而监听到数据变化
**解析器Compile**：解析Vue模板指令，将模板中的变量都替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，调用更新函数进行数据更新
**订阅者Watcher**：Watcher订阅者是Observer和Compile之间通信的桥梁，主要任务是订阅Observer中的属性变化值的消息，当收到属性值变化的消息时，触发解析器Compile中对应的更新函数。

订阅器采用**发布-订阅设计模式**，用来收集订阅者Watcher，对监听器Observer和订阅者Watcher进行统一管理
### vue3.0的响应式原理
改用**Proxy**替代Object.defineProperty
Proxy可以直接监听对象和数组的变化，并且有多达13种拦截方式，并且作为新标准将受到浏览器厂商重点持续的性能优化。
#### Proxy只会代理对象的第一层，vue3.0如何解决？
判断当前Reflect.get的返回值是否为Object，如果是则通过reactive方法做代理，这样就实现了深度观测
#### 监听数组的时候可能触发多次get/set,那么如何防止触发多次呢？
判断key是否为当前被代理对象target自身属性，也可以判断旧值和新值是否相等，只有满足以上两个条件之一，才可能执行trigger

### Proxy和Object.defineProperty的区别
Proxy的优点：
- 可以直接监听对象而非属性
- 可以直接监听数组的变化
- 有多达13种拦截方式
- 返回的是一个新对象，可以只操作新对象达到目的，而Object.defineProperty只能遍历对象属性直接修改
- 作为一个新标准，将受到浏览器厂商重点持续的性能优化（新标准的性能红利）

Object.defineProperty的优点
- 兼容性较好，支持IE9+，而Proxy存在浏览器兼容性问题，而且无法用polyfill磨平

## vue2.0 组件通信有哪些方式？:question:
- prop和emit
- evenBus
- project和inject
  
## v-if和v-show 有什么区别？
v-if直接判断，false的模块直接不显示
v-show 不管true还是false都会渲染这个dom，作用相当于display:none 
v-if适用于较少判断的，v-show适合频繁的切换，这样就不用重绘，性能较好。
## computed和watch的区别和运用的场景？
- computed 
  计算属性，依赖其他属性值，并且computed的值**有缓存**，只有它依赖的属性值发生改变，computed的值才发生改变；
- watch 
  - **没有缓存性**，更多的是观察的作用，类似于某些数据的监听回调，每当监听的数据变化时都会指向回调进行后续操作；
  - 深度监听对象的属性时，要打开**deep: true**,这样就会对对象的每一项进行监听

运用场景：
1. 当需要进行数值计算，且依赖于其他数据时，应该使用**computed**，这样可以利用computed的缓存性，避免每次获取值时都要重新计算
2. 当需要在数据变化时执行异步/开销较大的操作时，应该使用**watch**，限制我们
## 组件中的data为什么是一个函数？
## v-model是如何实现双向数据绑定的？

## nextTick的实现原理是什么？
## Vue事件绑定原理是什么？
## 为什么不建议用index作为key？
## Vue中组件的生命周期调用顺序是怎么样的？
beforeCreated,created,beforeMounted,mounted,beforeUpdate,update,beforeDestory,destory
## 在什么阶段才能访问操作DOM？
created,beforeMounted,mounted,update,beforeUpdate,beforeDestory
## 接口请求一般放在哪个生命周期中？
mounted，mounted可以请求结束后，可以直接挂载。
## vue路由有几种模式？他们的实现原理分别是什么？区别在哪？
路由模式：hash模式和history模式
- hash模式
- history模式
  url是直接斜杆的，需要后台nginx进行相应的配置。实现原理主要是通过history.pushState这个api

### hash和history的区别？
1. url地址不同，hash的带#，history不带#
2. hash模式刷新和history刷新不一样

## 路由懒加载是什么意思？如何实现路由懒加载？
## vue Router导航守卫有哪些？
全局守卫和局部路由守卫
## vuex是什么？
全局状态管理，每一个vuex应用的核心就是store(仓库)。store基本上是一个容器，它包含着vue应用中的大部分状态。

用到了js设计模式中的**单例模式**，就是不管创建多少个实例，它都只返回第一次所创建的那个实例。
vuex的状态存储是响应式的，当vue组件从store中读取状态时，若store的状态发生变化，那么相应的组件中的数据也会相应的更新。
改变store中的状态的唯一途径即使**显式地提交mutation**。这样可以方便跟踪每个状态的变化。
### vuex的组成
- State
  定义了应用状态的数据结构。设置默认的初始状态
- Getter
  允许组件从Store中获取数据，mapGetters辅助函数仅仅是将store中的getter映射到局部计算属性
- Mutation
  是唯一更改store中状态的方法，且必须是同步函数
- Action
  用于提交mutation，可以包含任意异步操作
- Module
  允许将单一的store拆分为多个store且同时保存在单一的状态树中

### 什么情况下使用vuex？
构建一个**中大型单页应用**时，使用Vuex能更好地在组件外管理状态。
简单应用的不推荐用vuex，可以用更简单的store模式。
### vuex和全局对象有什么区别？
1. vuex的状态存储是响应式的，全局对象只是存了数据。
2. 不能直接改变store中的状态

### 为什么vuex的mutation中不能做异步操作？
vuex的所有状态变更都是通过mutation，异步操作通过Action来提交mutation来实现，这样使得我们可以方便地跟踪每一个状态的变化，从而让我们能够实现一些工具帮助我们更好地了解我们的应用。
#### 为什么可以跟踪每个状态的变化？
因为每个mutation执行完毕后都会对应到一个新的状态变更，这样devtools就可以打个快照存下来，然后就可以实现time-travel了。如果mutation支持异步操作德华，就没有办法知道状态是何时更新的，无法很好的进行状态的追踪，给调试带来困难

## 说说vue和react的异同？
## 什么是mixin（混入）？
## vue模板编译原理知道吗？简单描述一下
## diff算法说一下
## 说一说对keep-alive的理解
## 说说对SSR的了解
## 对vue3.0的特性你有什么了解？

# 参考资料
- [Vue最全知识点（基础到进阶，覆盖vue3.0，持续更新整理，欢迎补充讨论）——（公众号——前端日志周刊）]()
