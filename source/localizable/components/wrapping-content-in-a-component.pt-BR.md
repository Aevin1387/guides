Sometimes, you may want to define a component that wraps content provided by other templates.

For example, imagine we are building a `blog-post` component that we can use in our application to display a blog post:

```app/templates/components/blog-post.hbs 

# {{title}}

<div class="body">
  {{body}}
</div>

    <br />Now, we can use the `{{blog-post}}` component and pass it properties
    in another template:
    
    ```handlebars
    {{blog-post title=title body=body}}
    

(See [Passing Properties to a Component](../passing-properties-to-a-component/) for more.)

In this case, the content we wanted to display came from the model. But what if we want the developer using our component to be able to provide custom HTML content?

In addition to the simple form you've learned so far, components also support being used in **block form**. In block form, components can be passed a Handlebars template that is rendered inside the component's template wherever the `{{yield}}` expression appears.

To use the block form, add a `#` character to the beginning of the component name, then make sure to add a closing tag. (See the Handlebars documentation on [block expressions](http://handlebarsjs.com/#block-expressions) for more.)

In that case, we can use the `{{blog-post}}` component in **block form** and tell Ember where the block content should be rendered using the `{{yield}}` helper. To update the example above, we'll first change the component's template:

```app/templates/components/blog-post.hbs 

# {{title}}

<div class="body">
  {{yield}}
</div>

    <br />You can see that we've replaced `{{body}}` with `{{yield}}`. This tells
    Ember that this content will be provided when the component is used.
    
    Next, we'll update the template using the component to use the block
    form:
    
    ```app/templates/index.hbs
    {{#blog-post title=title}}
      <p class="author">by {{author}}</p>
      {{body}}
    {{/blog-post}}
    

It's important to note that the template scope inside the component block is the same as outside. If a property is available in the template outside the component, it is also available inside the component block.