# CodeStyle_Frontend
Resource: https://v2.vuejs.org/v2/style-guide/index.html?redirect=true
## Priority A:Essential (Error Prevetion)
### Multi-word component names essential
Component names should always be multi-word, except for root App components, and built-in components provided by Vue, such as <transition> or <component>.

This prevents conflicts with existing and future HTML elements, since all HTML elements are a single word.

**Bad**
```javascript
Vue.component('todo', {
  // ...
})
export default {
  name: 'Todo',
  // ...
}
```
**Good**
```javascript
Vue.component('todo-item', {
  // ...
})
export default {
  name: 'TodoItem',
  // ...
}
```
### Component data essential
Component data must be a function.
When using the data property on a component (i.e. anywhere except on new Vue), the value must be a function that returns an object.

**Detailed Explanation**

**Bad**
```javascript
Vue.component('some-comp', {
  data: {
    foo: 'bar'
  }
})
export default {
  data: {
    foo: 'bar'
  }
}
```
**Good**
```javascript
Vue.component('some-comp', {
  data: function () {
    return {
      foo: 'bar'
    }
  }
})
// In a .vue file
export default {
  data () {
    return {
      foo: 'bar'
    }
  }
}
// It's OK to use an object directly in a root
// Vue instance, since only a single instance
// will ever exist.
new Vue({
  data: {
    foo: 'bar'
  }
})
```
### Prop definitions essential
Prop definitions should be as detailed as possible.
In committed code, prop definitions should always be as detailed as possible, specifying at least type(s).

**Bad**
```javascript
// This is only OK when prototyping
props: ['status']
```
**Good**
```javascript
props: {
  status: String
}
// Even better!
props: {
  status: {
    type: String,
    required: true,
    validator: function (value) {
      return [
        'syncing',
        'synced',
        'version-conflict',
        'error'
      ].indexOf(value) !== -1
    }
  }
}
```
## Priority B Rules: Strongly Recommended (Improving Readability)
### Self-closing componentsstrongly recommended
Components with no content should be self-closing in single-file components, string templates, and JSX - but never in DOM templates.
Components that self-close communicate that they not only have no content, but are meant to have no content. It’s the difference between a blank page in a book and one labeled “This page intentionally left blank.” Your code is also cleaner without the unnecessary closing tag.
Unfortunately, HTML doesn’t allow custom elements to be self-closing - only official “void” elements. That’s why the strategy is only possible when Vue’s template compiler can reach the template before the DOM, then serve the DOM spec-compliant HTML.

**Bad**
```html
<!-- In single-file components, string templates, and JSX -->
<MyComponent></MyComponent>
<!-- In DOM templates -->
<my-component/>
```
**Good**
```html
<!-- In single-file components, string templates, and JSX -->
<MyComponent/>
<!-- In DOM templates -->
<my-component></my-component>
```
### Multi-attribute elementsstrongly recommended
Elements with multiple attributes should span multiple lines, with one attribute per line.
In JavaScript, splitting objects with multiple properties over multiple lines is widely considered a good convention, because it’s much easier to read. Our templates and JSX deserve the same consideration.

**Bad**
```html
<img src="https://vuejs.org/images/logo.png" alt="Vue Logo">
<MyComponent foo="a" bar="b" baz="c"/>
```
**Good**
```html
<img
  src="https://vuejs.org/images/logo.png"
  alt="Vue Logo"
>
<MyComponent
  foo="a"
  bar="b"
  baz="c"
/>
```

### Quoted attribute valuesstrongly recommended
Non-empty HTML attribute values should always be inside quotes (single or double, whichever is not used in JS).
While attribute values without any spaces are not required to have quotes in HTML, this practice often leads to avoiding spaces, making attribute values less readable.

**Bad**
```html
<input type=text>
<AppSidebar :style={width:sidebarWidth+'px'}>
```
**Good**
```html
<input type="text">
<AppSidebar :style="{ width: sidebarWidth + 'px' }">
```
## Priority C Rules: Recommended (Minimizing Arbitrary Choices and Cognitive Overhead)
### Component/instance options order recommended
Component/instance options should be ordered consistently.
This is the default order we recommend for component options. They’re split into categories, so you’ll know where to add new properties from plugins.

1.**Side Effects** (triggers effects outside the component)

el

2.**Global Awareness** (requires knowledge beyond the component)

name
parent

3.**Component Type** (changes the type of the component)

functional

4.**Template Modifiers** (changes the way templates are compiled)

delimiters
comments

5.**Template Dependencies** (assets used in the template)

components
directives
filters

6.**Composition** (merges properties into the options)

extends
mixins

7.**Interface** (the interface to the component)

inheritAttrs
model
props/propsData

8.**Local State** (local reactive properties)

data
computed

9.**Events** (callbacks triggered by reactive events)

watch
Lifecycle Events (in the order they are called)
beforeCreate
created
beforeMount
mounted
beforeUpdate
updated
activated
deactivated
beforeDestroy
destroyed

10.**Non-Reactive Properties** (instance properties independent of the reactivity system)

methods

11.**Rendering** (the declarative description of the component output)

template/render
renderError
