# Learning-vue2
My short note, in lacture Vue.js 2 class

## [ Learning Vue ]
```
   let data ={
     message: 'Hi, I will be a front-end expert!.'
   };
   document.querySelector('#input1').value = data.message;
```

## [ Learning Vue: 002 ]
```
 new Vue({
   el: '#root',
   data: {
     message: 'a front-end expert!.',
     foo: 'some texts'
   }
 })
```

## [ Learning Vue: 003 ARRAY ]
** html **
```
<div id="root">
   <ul>
     <li v-for="name in names" v-text="name"></li>
   </ul>
   <input type="text" v-model="newName">
   <button v-on:click="addName">ADD</button>
</div>
```

** VUE **

```
var app = new Vue({
  el: '#root',
  data: {
    newName: '',
    names: ['Joe', 'Mary', 'Jane', 'Bank', 'Me']
  },
  // method obj.
  methods: {
    //method name
          // old addName: function(){} or
    addName() {
      // alert('adding name');
      this.names.push(this.newName);
      // clear input box
      this.newName = '';
    }
  }
});
```

try a fun tool: adding a VUE extention for chrome or VUE add-on (firefox-dev)

1. call $vm0 in console and see result
2. add var app ==
3. call app then see result
4. how to [add new ARRAY by] app.names.push('Susan');

#### ====the ES6 way=====

- add id in input and btn
- use ES6 way


```
document.querySelector('#button').addEventListener('click', () => {
let name = document.querySelector('#input');
  app.names.push(name.value);
  name.value = '';
});
```
**or**

>
```
mounted(){
    put javascript in here
}
```
eg.
```
mounted(){
   document.querySelector('#button').addEventListener('click', () => {
     let name = document.querySelector('#input');
     app.names.push(name.value);
     name.value = '';
   });
 }
```
**or**

> use v-on:click=""


## +++++++[ Learning Vue: 004 attribute binding]++++++++
** html **
```
var app = new Vue({
  el: '#root',
  data: {
    titleObj: 'NEW U SEE ME....'
  }
});
```
** VUE **
```
<div id="root">
   <button v-bind:title="titleObj">Hover Me</button>
</div>
```
>v-bind bind attribute "title" to show whatever titleObj collect
v-bind:title="titleObj"

**a normal**
** VUE **
```
<button v-on:click="methodName" v-bind:title="titleObj">Hover Me</button>
```
**a shorter**
** VUE **
```
 <button @click="methodName" :title="titleObj">Hover Me</button>
```
## [ Learning Vue: 005 class style]

use :class="className" to change a classname

** html **
```
<div id="root">
   <h1 :class="className">Yeah, I am yellowing.</h1>
</div>
```

** css **
```
.be-yellow{
  color: yellow;
}
```
** VUE **
```
var app = new Vue({
  el: '#root',
  data: {
    className: 'be-yellow'
  }
});
```


## [ Learning Vue: 006 ]

** html **
```
<h1> Hi,  {{ msg.split('').reverse().join('')}} </h1>
```
** VUE **
```
var app = new Vue({
  el: '#root',
  data: {
    msg: 'Sweety'
  }
});
```
**or**
** html **
```
<div id="root">
   <h1> Hi, Turn this {{ msg }} to this {{ reversedMsg }} </h1>
</div>
```
** VUE **
```
var app = new Vue({
  el: '#root',
  data: {
    msg: 'Sweety'
  },
    //called computed propoties
  computed: {
    reversedMsg() {
      return this.msg.split('').reverse().join('');
    }
  }
});
```



## [ Learning Vue: 007 Let's make a collection of tasks]
** html **
```
<ul>
  <li v-for="task in tasks" v-if="task.completed" v-text="task.description"></li>
</ul>
```
** VUE **
```
var app = new Vue({
  el: '#root',
  data: {
    tasks: [
      { description: 'Go to the market', completed: true },
      { description: 'Go to the rastaurent', completed: false },
      { description: 'Clean a room', completed: true },
      { description: 'But some fruits', completed: false },
      { description: 'Get up early', completed: true },
      { description: 'Do abs, legs, arms workout', completed: false }
    ]
  }
});
```

**or use a computed propoties do filter**

** html **
```
<div id="root">
   <h1>Mini Todo list</h1>
   <h2>all tasks</h2>
   <ul>
     <li v-for="task in tasks" v-text="task.description"></li>
   </ul>
     <h2>incompleted tasks</h2>
   <ul>
     <li v-for="task in incompletedTasks" v-text="task.description"></li>
   </ul>
</div>
```
** VUE **
```
var app = new Vue({
  el: '#root',
  data: {
    tasks: [
      { description: 'Go to the market', completed: true },
      { description: 'Go to the rastaurent', completed: false },
      { description: 'Clean a room', completed: true },
      { description: 'But some fruits', completed: false },
      { description: 'Get up early', completed: true },
      { description: 'Do abs, legs, arms workout', completed: false }
    ]
  },
  computed: {
    incompletedTasks() {
      return this.tasks.filter(task => ! task.completed);
    }
  }
});
```
>
===es6===

this.tasks.filter(function (task){
  return task.completed
})

===or===

this.tasks.filter(task => ! task.completed);

## +++++++[ Learning Vue: 008 Components Things ]++++++++

basic concept: to reuse a element: card, nav, button, another button etc.
[basic structure about component]
create component called 'task'
then using it as html tag <task></task>

** html **
```
<div id="root">
  <task>task</task>
  <task>another task</task>
</div>

```
** VUE **
```
Vue.component('task', {
    template: '<li><slot></slot></li>'
});
new Vue({
  el: '#root'
})
```


### [ Components in Components]

** html **
```
<div id="root">
  <task-list></task-list>
</div>
```

** VUE **
```
Vue.component('task-list', {
    template: `
    <div>
      <task v-for="task in tasks">{{ task.task }}</task>
    </div>
    `,

    data() {
      return {
        tasks: [
          { task: 'Go to the market', complete: true },
          { task: 'Go to the rastaurent', complete: false },
          { task: 'Clean a room', complete: true },
          { task: 'Buy some fruits', complete: false },
          { task: 'Get up early', complete: true },
          { task: 'Do abs, legs, arms workout', complete: false }
        ]
      };
    }
});

Vue.component('task', {
    template: '<li><slot></slot></li>'
});

new Vue({
  el: '#root'
})
```

--Note--

//cannot use root element render multiple element

```<task v-for="task in tasks">{{ task.task }}</task>```

// try this instead

```<div>
  <task v-for="task in tasks">{{ task.task }}</task>
</div>```


## +++++++[ Learning Vue: 00 ]++++++++
** html **
```

```
** VUE **
```

```

## +++++++[ Learning Vue: 00 ]++++++++
** html **
```

```
** css **
```

```
** VUE **
```

```


## +++++++[ Learning Vue: 00 ]++++++++
** html **
```

```
** css **
```

```
** VUE **
```

```
