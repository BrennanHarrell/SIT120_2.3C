<script setup>
import { ref, computed, watch } from 'vue'
import PersonComp from "../components/PersonComp.vue";

// 1. Template Syntax
const todo = ref("");
const interp = ref("Webapp");
const rawHtml = ref("rawHtml");
const htmlBind = ref("");
const javaExpress = ref("Java Expression");

const count = ref(0);
const methodValue = ref(0);
const errorColor = ref("red");
const textSize = ref (30);
const checkError = ref(true);

// 2. Methods
const increase = () => {
     methodValue.value++
   };
const decrease = () => {
    methodValue.value--
   };

// 3. Ractivity
const reactivityValue = ref(2);

function inc() {
 reactivityValue.value = reactivityValue.value * 2;
};

// 4. Computed property
const computedValue = computed(() => {
    if (methodValue.value % 2 === 0) return 'even'
    return 'odd'
})

// 6. List Rendering 
const items = ref([{ message: 'v-for' }, { message: 'with an' }, { message: 'object' }]);

const vforArray = ref([
 "templaye syntax",
 "methods",
 "reactivity",
 "list rendering",
 "event handling",
]);
 
const vforIndex = ref(0);

const items1 = ref([{ message: 'v-if and v-for' }, {message: "error detected"}]);
// End List Rendering 


// 7.b method handling function
function methodHandler(event) {
 alert("Injection attack detected")
};

// used for v-model
const newItem = ref("");
const newMessage = ref("");
const age = ref();

// 9. Watcher
watch(methodValue, (newValue) => {
     if(newValue === 10) {
       alert ("Count has hit 10")
     }
    });

// 10.b Event [$emit]
const showAlert = () => {
    alert("Emit Check")
};

</script>

<template>

  <!--1. All TEMPLATE SYNTAX --> 
  <!--1.a Text Interpolation--> 
 <div>This my {{ interp }}</div>

 <!--1.b Raw HTML--> 
 <p>Here is some: <span v-html="rawHtml"></span></p>

 <!--1.c Attribute Binding --> 
 <h2 v-bind:="htmlBind">Using HTML h2</h2>

 <!--1.d JavaScript Expression --> 
 {{ javaExpress.toUpperCase() }}
  <!-- End Template syntax --> 

 <!--2. METHOD --> 
 <div>
   <p>Method:</p>
   <button @click="decrease()">-</button>
   <span> {{ methodValue }}</span>
   <button @click="increase()">+</button>
 </div>
 <!-- END Method --> 

 <!--3. REACTIVITY FUNCTIONALITY --> 
 <div>
   <p>Reactivity Functionality:</p>
   <button @click="inc()">Incementing count: {{ reactivityValue }}</button>
 </div>
 <!-- END Reactivity Functionality --> 

  <!--4. COMPUTED PROPERTY --> 
 <div>
    <p>method value is {{ computedValue }}</p>
 </div>

 <!--5. CLASS AND STYLE BINDINGS --> 
 <!--5.a Binding HTML class  --> 
 <div>
   <button v-on:click="checkError=!checkError">Class binding</button>
   <h2 :class="{noError:checkError,Error:!checkError}">Class Binding</h2>
 </div>

 <!--5.b Binding Inline Style --> 
 <div>
   <h2 v-bind:style="{
   color: errorColor,
   'font-size': textSize + 'px',
   textAlign: 'right',
 }">Instyle Binding</h2> 

 </div>
 <!-- END Class and Bind styling --> 

 <!--6. LIST RENDERING --> 

 <!--6.a V-for with an object --> 
 <li v-for="item in items" v-bind:key="item.id">
   {{ item.message }}
 </li>

 <!--6.b/c v-for with range and on template --> 
 <div>
   <template v-for="i in 2"  v-bind:key="i">
   <p>v-for with range + template</p>
   <li >
   {{ vforArray[vforIndex * 2 + i] }}
   </li>
   </template>
 </div>

 <!--6.d v-for with v-if --> 
 <div>
   <template v-for="item in items1" v-bind:key="item.id">
     <li v-if="!checkError">
       {{ item.message }}
     </li>
   </template>
 </div>

 <!--6.e v-for with a component--> 
 <div>
   <ul>
   <some-item
     v-for="(item, index) in items"
     :key="item.id"
     :title="item.title"
     @remove="item.splice(index, 0)"
   ></some-item>
   <li>
   {{ title }}
   </li>
   </ul>
 </div>
 <!-- END List Rendering --> 

 <!--7. EVENT HANDLING --> 
 <!--7.a Inline Handling --> 
 <div>
   <button @click="count++">Inline Handling</button>
   <p>Count is: {{ count }}</p>
 </div>

 <!--7.b Method handling --> 
 <div>
   <button @click="methodHandler">Method Handling</button>
 </div>
 <!-- END Event Handling --> 
 
 <!-- FORM INPUT BINDINGS --> 
 <!-- v-model --> 
 <div>
   <h2>V-model</h2>
   <!-- input type="checkbox" --> 
   <input v-model.number="newItem" type="checkbox">
   <!-- input type="radio" --> 
   <input v-model="newItem" type="radio">
   <br>
   <!-- input type="text" --> 
   <input v-model.trim="newItem" type="text">
   <!-- v-model <select> --> 
   <select v-model="newItem">
     <option value="low">low</option>
     <option value="high">high</option>
   </select>
   <br>
   <!-- input type="number" --> 
   <input v-model.number="age" type="number">
   <br>
   <!-- v-model <textarea> --> 
   <textarea v-model.lazy="newMessage" placeholder="give feedback on functionality"></textarea>
   {{ newItem }}
   {{ age }}
   {{ newMessage }}
 </div>
   <!-- END Form Input Binding ALL --> 
   
   <!--9. Watcher copied from below Watch: > 
   watch: {
   methodValue(newValue) {
     if(newValue === 10) {
       alert ("Count has hit 10")
     }
   --> 

   <!--10. COMPONENTS --> 

   <!--10.a/b Prop and $Emit Components copied from PersonComp.vue

    Prop
    const props = defineProps({
    text: {
        type: String,
        required: true,
    }

    Emit
    const emit = defineEmits(['emitCheck'])

    });

    <div>
        <button @click="$emit('emitCheck')">{{ text }}</button>
    </div>

-->

   
   <!--10.c SLOT PeronComp.vue

    Copied from NewComp.vue
    <div>
       <img src="https://i.stack.imgur.com/y9DpT.jpg"  />

       <p>
        <slot name="Caption">Caption for Image</slot>

       </p>

    </div>

    Copied from PeronComp.vue
    <NewComp>
    <template #Caption>
        Image not loading
    </template>
    </NewComp>

    
    --> 

    <div>
        <PersonComp @emitCheck="showAlert" 
        text="Component Prop" />
    </div>


</template>