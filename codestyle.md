# CodeStyle
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
