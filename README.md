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
**html**
```
<div id="root">
   <ul>
     <li v-for="name in names" v-text="name"></li>
   </ul>
   <input type="text" v-model="newName">
   <button v-on:click="addName">ADD</button>
</div>
```

**VUE**

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


## [ Learning Vue: 004 attribute binding ]
**html**
```
var app = new Vue({
  el: '#root',
  data: {
    titleObj: 'NEW U SEE ME....'
  }
});
```
**VUE**
```
<div id="root">
   <button v-bind:title="titleObj">Hover Me</button>
</div>
```
>v-bind bind attribute "title" to show whatever titleObj collect
v-bind:title="titleObj"

**a normal**
**VUE**
```
<button v-on:click="methodName" v-bind:title="titleObj">Hover Me</button>
```
**a shorter**
**VUE**
```
 <button @click="methodName" :title="titleObj">Hover Me</button>
```
## [ Learning Vue: 005 class style]

use :class="className" to change a classname

**html**
```
<div id="root">
   <h1 :class="className">Yeah, I am yellowing.</h1>
</div>
```

**css**
```
.be-yellow{
  color: yellow;
}
```
**VUE**
```
var app = new Vue({
  el: '#root',
  data: {
    className: 'be-yellow'
  }
});
```


## [ Learning Vue: 006 ]

**html**
```
<h1> Hi,  {{ msg.split('').reverse().join('')}} </h1>
```
**VUE**
```
var app = new Vue({
  el: '#root',
  data: {
    msg: 'Sweety'
  }
});
```
**or**

**html**
```
<div id="root">
   <h1> Hi, Turn this {{ msg }} to this {{ reversedMsg }} </h1>
</div>
```
**VUE**
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

**html**
```
<ul>
  <li v-for="task in tasks" v-if="task.completed" v-text="task.description"></li>
</ul>
```
**VUE**
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

**html**
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

**VUE**
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

===es6===

this.tasks.filter(function (task){
  return task.completed
})

===or===

this.tasks.filter(task => ! task.completed);

## Learning Vue: 008 Components Things

basic concept: to reuse a element: card, nav, button, another button etc.
[basic structure about component]
create component called 'task'
then using it as html tag <task></task>

**html**
```
<div id="root">
  <task>task</task>
  <task>another task</task>
</div>

```

**VUE**
```
Vue.component('task', {
    template: '<li><slot></slot></li>'
});
new Vue({
  el: '#root'
})
```


### [ Components in Components]

**html**
```
<div id="root">
  <task-list></task-list>
</div>
```

**VUE**
```
Vue.component('task-list', {
    template: `
    <ul>
      <task v-for="task in tasks">{{ task.task }}</task>
    </ul>
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

cannot use root element render multiple elements

```<task v-for="task in tasks">{{ task.task }}</task>```

// try this instead: add ul tag

```<ul>
  <task v-for="task in tasks">{{ task.task }}</task>
</ul>
```

#### [ Components exercise vol.1 ]

This exercise is power by BULMA.
Using vue create a components.
- add https://cdnjs.cloudflare.com/ajax/libs/bulma/0.4.3/css/bulma.css
- choose your element: I choose a message components.
- and then, repeating it by yourself

**html**
```
<div id="root">
  <h3>the old by html</h3>
  <article class="message">
    <div class="message-header">
      <p>Hello World</p>
      <button class="delete"></button>
    </div>
    <div class="message-body">
      Lorem ipsum dolor sit amet, consectetur adipiscing elit. <strong>Pellentesque risus mi</strong>, tempus quis placerat ut, porta nec nulla. Vestibulum rhoncus ac ex sit amet fringilla. Nullam gravida purus diam, et dictum <a>felis venenatis</a>        efficitur. Aenean ac <em>eleifend lacus</em>, in mollis lectus. Donec sodales, arcu et sollicitudin porttitor, tortor urna tempor ligula, id porttitor mi magna a neque. Donec dui urna, vehicula et sem eget, facilisis sodales sem.
    </div>
  </article>
    <hr>
<h3>the new by vue</h3>
    <message title="Hi, I am a best one." body="Lorem ipsum dolor sit amet, consectetur adipiscing elit. "></message>
    <message title="Hello" body="text in body, YEAH!!!!"></message>
</div>
```

**VUE**
```
Vue.component('message', {
  props: ['title', 'body'],
    template: `
    <article class="message">
      <div class="message-header">
        {{ title }}
      </div>
      <div class="message-body">
        {{ body }}
      </div>
    </article>
    `
});

new Vue({
  el: '#root'
})
```

-- note: --
first we try to pass title and body props(propoties)
will get:

>[Vue warn]: Property or method "title" is not defined on the instance but referenced during render. Make sure to declare reactive data properties in the data option.

we need to declare a props to make a component accept by adding:

```
...
props: ['title', 'body'],
...
```

##### [ Components exercise vol.1: close BTN ]

--note1.--
create a close-btn, there are many way eg.

update code below

**html**
```
<div id="root">
  <message title="Hi, I am a best one." body="Lorem ipsum dolor sit amet, consectetur adipiscing elit. "></message>
  <message title="Hello" body="text in body, YEAH!!!!"></message>
</div>
```

**VUE**
```
Vue.component('message', {
  props: ['title', 'body'],

  data() {
    return {
        isVisible: true
    };
  },

    template: `
    <article class="message" v-show="isVisible">
      <div class="message-header">
        {{ title }}
        <button type="button" @click="hideModal">x</button>
      </div>
      <div class="message-body">
        {{ body }}
      </div>
    </article>
    `,

    methods: {
      hideModal() {
        this.isVisible = false;
      }
    }

});

new Vue({
  el: '#root'
})
```

- using method and and add jquery to do: hide, toggleClass, etc.

```
...
method: {
    hideModal() {
      $('.message').hide();
    }
  }
...
```

--or--

- return an obj. in data

```
...
data() {
  return {
      isVisible: true
  };
},
...
```

and then use directive => [v-show=""](do not hide an element if true/false )


```
...
template: `
<article class="message" v-show="true">
...
```

in lesson we gonna bind v-show with "isVisible"

```
...
template: `
<article class="message" v-show="isVisible">
...
```

--note2.--

we can reuse v-show="isVisible" anywhere

```
...
<button type="button" @click="isVisible = false">x</button>
...
```



##### [ Learning Vue: Components exercise vol.2: Modal ]

we're going to learn how to communicate between components.



**html**
```

  <div id="root">

    <modal v-if="showModal" @close= "showModal = false">
      <p> Now, we have a one part so we use slot tag instead </p>
    </modal>

    <button type="button" @click="showModal = true">Show a magic.</button>


  </div>
```

In HTML : binding element modal: using v-if or v-show

**VUE**
```
Vue.component('modal', {

  template: `

    <div class="modal is-active">
      <div class="modal-background"></div>
      <div class="modal-content">
        <div class="box">
          <slot></slot>
        </div>
      </div>
      <button class="modal-close is-large" @click="$emit('close')"></button>
    </div>

  `,

});

new Vue({
  el: '#root',
  data: {
    showModal: false
  }
})
```



--note 1.--

normally we can use @click="showModal = false" in to make it close modal
but showModal has it own scope(can not be use in )

so we need to announce $emit('close') when click

first, attached @close at modal

```
...
<modal v-if="showModal" @close= "showModal = false"></modal>
...
```

and then add $emit('close') on close btn

```
...
<button class="modal-close is-large" @click="$emit('close')"></button>
...
```

so clicking a close btn it will admit a [@close= "showModal = false"] ,which is update showModal to false


--note 2.--

we need to add "is-active" at modal

--note 3.--

we can use [props] to define a model content (more example in previous lesson): modal's title, modal's body or modal's footer if it have more than one
but now it has one part, so we use slot tag instead in html

```
...
<slot></slot>
...
```

##### [ Learning Vue: Components exercise vol.3: Tabs ]
**html**
```
<div id="root">
    <tabs>
      <tab name="About Us" :selected="true">
        <p>Here is a content for about us tab</p>
      </tab>
      <tab name="Our Service">
        <p>Here is a content for our service tab</p>
      </tab>
      <tab name="Contact Us" >
        <p>Here is a content for contact us tab</p>
      </tab>
    </tabs>
</div>
```
**VUE**
```
Vue.component('tabs', {

  template: `
    <div class="tabs-wrapper">
        <div class="tabs">
          <ul>
            <li v-for="tab in tabs" :class="{ 'is-active' : tab.isActive }">
              <a :href="tab.href" @click="selectTab(tab)">{{ tab.name }}</a>
            </li>
          </ul>
        </div>
        <div class="tabs-details">
          <slot></slot>
        </div>
      </div>
  `,

    // mounted() {
    //   console.log(this.$children);
    // },
  data() {
    return{
      tabs: []
    };
  },
  created() {
    this.tabs = this.$children;
  },
  methods: {
    selectTab(selectedTab){
      this.tabs.forEach(tab => {
          // tab.selected = (tab.name == selectedTab.name)
          tab.isActive = (tab.name == selectedTab.name)
      });

    }
  }

});

Vue.component('tab',{

  template: `
    <div v-show="isActive"><slot></slot></div>
  `,

  props: {
    name: { required: true },
    selected: { default: false }
  },
  data() {
    return{
      isActive: false
    };
  },
  computed: {
    href() {
      return '#' + this.name.toLowerCase().replace(/ /g, '-');
    }
  },
  mounted() {

    this.isActive = this.selected;

  }

});

new Vue({
  el: '#root',
})

```

using to log what is inside a tabs , a result: we will not see anything

```
...
mounted() {
  console.log(this.$children);
}
...
```

so we need to add slot tab, right now in log we can see a tab details in side a tabs

```
...
<div class="tabs-details">
  <slot></slot>
</div>
...
```

and then we need to wrap tag both tabs tag and tab tag because these will render multi element
by adding

```
...
  <div class="tabs-wrapper">
    ...
        <div class="tabs">
        ...
        <div class="tabs-details">
        ...
  </div>
...
```

vue log will display Unknow custom element <tab>
because we didn't define tab component yet so define it by

```
...
  Vue.component('tab',{
    template: `
      <div>
        <slot></slot>
      </div>
    `
  });
...
```

see log: now there are Objs in tabs.

In a tab component. We use [props] required = true as a ID

```
...
  props: {
    name: {
      required: true
    }
  }
...
```

see log again: try in vue extention [$vm0.$children.forEach(tab => console.log(tab.name));]
log a name of each tab

```
...
  About Us
  Our Service
  Contact Us
...
```

now we can grab name in each tab by adding in created() in tabs to make a tabs component create a tab
 and the return it by data()

```
...
  data() {
    return{
      tabs: []
    };
  },

  created() {
    this.tabs = this.$children;
  }
...
```

now at tab instance we can see obj, in tabs


Next: we need to clean tab list by change this

```
...
  <ul>
    <li class="is-active"><a>Pictures</a></li>
    <li><a>Music</a></li>
    <li><a>Videos</a></li>
    <li><a>Documents</a></li>
  </ul>
...
```

to this: Using v-for=""

```
...
  <li v-for="tab in tabs">
    <a href="#">{{ tab.name }}</a>
  </li>
...
```

We need to set a class .active by default and dynamiclly

1. add selected: {} in tab component
```
...
  props: {
    name: { required: true },
    selected: { default: false }
  }
...
```

2. in li tag : Bind the class to (:class), and set a class (.is-active)
if a tab is selected (: tab.selected)
```
...
    <li v-for="tab in tabs" :class="{ 'is-active' : tab.selected }">
...
```

3. Make it toggleClass: by add @click
```
...
    <a href="#" @click="selectTab(tab)">{{ tab.name }}</a>
...
```

then test in tabs component

```
...
  methods: {
    selectTab(){
      alert("tab is selected!!!");
    }
  }
...
```

But we need to change class dynamiclly so in tab component add data() and mounted() to link it into class

```
...
data() {
  return{
    isActive: false
  };
},
mounted() {
  this.isActive = this.selected;
}
...
```

then change selected to isActive (2.) and (3.)

Now, data function should return an obj and a tab button is working!!!!
https://laracasts.com/series/learn-vue-2-step-by-step/episodes/11
(at: 12.00 sec)

-- Make tab body show a text --
Using v-show="": show what is in slot tag when current tab is selected or active


```
...
  template: `
    <div v-show="isActive"><slot></slot></div>
  `,
...
```

-- Finally, tab component is perfect. --

###### optional for tab link : binding a href

in template
```
...
  <a :href="tab.herf" @click="selectTab(tab)">{{ tab.name }}</a>
...
```

then using a computed() props to create a link(#XXX)
: add # , turn txt to lower case and replace a space with dash(-)



```
...
    computed: {
      href() {
        return '#' + this.name.toLowerCase().replace(/ /g, '-');
      }
    },
...
```

Result:

About Us >>>> #about-us

<a href="#about-us">About Us</a>


more infomation about vue life cycle https://alligator.io/vuejs/component-lifecycle


## [ Learning Vue: Custom Components: vol.1 ]
communicate between parent tag/element and child tag/element

**html**
```
<div id="root">
  <coupon @applied="onCouponApplied"></coupon>
  <hr>
    <h4 v-if="couponApplied">You used a coupon.</h4>
</div>
```


**VUE**
```
Vue.component('coupon',{
  template: `
    <input placeholder="Enter your coupon code" @blur="onCouponApplied">
  `,
  methods: {
    onCouponApplied() {
      this.$emit('applied')
    }
  }
});


new Vue({
  el: '#root',
  data: {
    couponApplied: false
  },
  methods: {
    onCouponApplied() {
      this.couponApplied = true;
    }
  }
})
```

-- reorder  --
if we declare a component after New Vue...

Log:
[Vue warn]: Unknown custom element: <coupon> - did you register the component correctly?

so

```
...
Vue.component('coupon',{
  template: `
    <input type="text">
  `,
});
new Vue({
  el: '#root',
  methods: {
    onCouponApplied() {
    alert('Applied!');

    }
  }
})
...
```

add this add then try typing in textbox and the enter: it will alert text
```
...
Vue.component('coupon',{
  template: `
    <input placeholder="Enter your coupon code" @blur="onCouponApplied">
  `,
  methods: {
    onCouponApplied() {
      alert('Applied!');
    }
  }
});
...
```

then u can pass Obj. or pass etc.
```
...
this.$emit('coupon-was-applied', this.coupon)
...
```

then, try typing again: In this case parent tag/element do a method
when coupon applied it will alert a message ('It was applied!')

-- optional --
try this
VUE
```
...
data: {
  couponApplied: false
},
methods: {
  onCouponApplied() {
    this.couponApplied = true;
  }
}
...
```

html
```
...
<h4 v-if="couponApplied">You used a coupon.</h4>
...
```

## [ Learning Vue: Custom Components: vol.2 ]
communicate between another node: sibling, coupon notify another one,  ETC.
**HTML**
```
<div id="root">
  <coupon @applied="onCouponApplied"></coupon>
  <hr>
    <!-- <h4 v-if="couponApplied">You used a coupon.</h4> -->
</div>
```

**VUE**
```
window.Event = new Vue();

Vue.component('coupon',{
  template: `
    <input placeholder="Enter your coupon code" @blur="onCouponApplied">
  `,
  methods: {
    onCouponApplied() {
       Event.$emit('applied');
    }
  }
});


new Vue({
  el: '#root',
  data: {
    couponApplied: false
  },
  // methods: {
  //   onCouponApplied() {
  //     this.couponApplied = true;
  //   }
  // }
  created() {
    Event.$on('applied', () => alert('Handling it!!!!'))
  }
})

```

## [ Learning Vue: Named Slots in a Nutshell ]

more details about slot tag to perfect template

-- Note 1. --
use template tag if you don't want div tag

**html**
```
<div id="root">
  <modal>
    <template slot="header">This is a title.</template>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Incidunt, maxime ullam quae illo amet nihil facere provident illum officiis delectus explicabo vero molestias perferendis reiciendis quaerat, ut, deserunt dolores. Rerum.
    <div slot="footer">
      <a class="button is-success">Save changes</a>
       <a class="button">Cancel</a>
    </div>
  </modal>
</div>
```

**VUE**
```
Vue.component('modal',{
  template: `

    <div class="modal is-active">
      <div class="modal-background"></div>
        <div class="modal-card">

          <header class="modal-card-head">
            <p class="modal-card-title">
              <slot name="header"></slot>
            </p>
            <button class="delete"></button>
          </header>

          <section class="modal-card-body">
            <slot></slot>
          </section>

          <footer class="modal-card-foot">
            <div slot="footer">
               <a class="button is-success">Okay</a>
            </div>
          </footer>

        </div>
      </div>

  `,
});

new Vue({
  el: '#root',
  data: {
  },
})
```
-- Note 2. --
use a slot tag to make a default content in side html tag


# SOON 

## [ Learning Vue: 00 ]
**html**
```

```
**css**
```

```
**VUE**
```

```


## [ Learning Vue: 00 ]
**html**
```

```
**css**
```

```
**VUE**
```

```
