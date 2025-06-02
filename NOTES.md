#### Starting our server

In our terminal we type

npm run dev

This will then open a browser on our computer at http://localhost:3000

#### First Component

We can define our page using either a function declaration or a function expression.
You will see both been used. The key is to choose one and stick to it throughout your app.

We will use the function function expression as it is easier to read and recognise and is more
popular in modern codebases.

### A function declaration

```js
export default function FirstComponent() {
  return <h1>About</h1>;
}
```

### A function expression

```js
const FirstComponent = () => {
  return <h1>About</h1>;
};

export default FirstComponent;
```

- The component name should start with a capital letter
- must return JSX (html)
- when we call a component we must use a closing tag <FirstComponent/>
- must use export
- all components are functions

### JSX rules

JSX is a syntax extension for JavaScript that lets you write HTML-like code inside your JavaScript. It’s used in React to describe what the UI should look like.

- we must always, always return a single element (one parent element)

```js
//this will not work, as we do not have one parent element
const FirstComponent = () => {
  return (
    <section>
      <h2>My first book</h2>
      <p>This is a very good book</p>
    </section>
    <h2>A new title</h2>
  );
};

export default FirstComponent;

```

- fragments alllow us toe group elements together without adding extra nodes.

```js
//this will work, as we have added a fragment
const FirstComponent = () => {
  return (
    <>
      <section>
        <h2>My first book</h2>
        <p>This is a very good book</p>
      </section>
      <h2>A new title</h2>
    </>
  );
};

export default FirstComponent;
```

- we should use the approriate html semantics e.g. section/article/aside

- camelCase property naming convention

```js
//in jsx
//note the attributes
return (
  <div tabIndex={1}>
    <button onClick={myFunction}>click me</button>
    <label htmlFor='name'>Name</label>
    <input readOnly={true} id='name' />
  </div>
)
// in html
//note the attributes
<div tabindex="1">
    <button onclick="myFunction()">click me</button>
    <label for='name'>Name</label>
    <input readonly id='name' />
</div>
```

-- className not class (class is a reserved word in React)

- close every element

```js
return <img />;
// or
return <input />;
```

- formatting
  - opening tag in the same line as return or ()

```js
export const Howdy()=>{
  return <div>Howdy everyone</div>

}
```

OR

```js
export const Howdy()=>{
  return (
    <div>Howdy Everyone</div>
  )
}
```

Note: if were to use vanilla js to write what we are trying to return in the JSX it would look like this. JSX makes our life a lot easier.

```js
function FirstComponent() {
  const section = document.createElement('section');

  const h2InSection = document.createElement('h2');
  h2InSection.textContent = 'My first book';

  const p = document.createElement('p');
  p.textContent = 'This is a very good book';

  section.appendChild(h2InSection);
  section.appendChild(p);

  const secondH2 = document.createElement('h2');
  secondH2.textContent = 'A new title';

  // Return both elements as an array
  return [section, secondH2];
}

// Rendering to the DOM
const root = document.getElementById('root');
const elements = FirstComponent();

elements.forEach(el => root.appendChild(el));
```

#### Nesting our components.

Let's consider this component

```js
const Greeting() => {
  return (
    <div>
      <h2>Jane Doe</h2>
      <p>a personal message</p>
    </div>
  )

}
export default Greeting;
```

If we decide we want to make the h2 and p elements reuseable components in their own right.

```js
const Greeting = () => {
  return (
    <div>
      <Person />
      <Message />
    </div>
  );
};

export default Greeting;

const Person = () => <h2>Jane Doe</h2>;
const Message = () => <p>A personal message</p>;
```

Why would we want to do this?

- we may have many people we want to send a message to and so we will want to only create the component once, but send data to the component of all the people we know and the compoenent would render for each person.
  This will become clearer as the course progresses.

- it could also be for performance reasons, but again this will become clearer as we progress.

#### Importing our components into the parent

```js
import Person from '@/components/person';
import Message from '@/components/message';

const Greeting = () => {
  return (
    <div>
      <Person />
      <Message />
    </div>
  );
};

export default Greeting;
```
