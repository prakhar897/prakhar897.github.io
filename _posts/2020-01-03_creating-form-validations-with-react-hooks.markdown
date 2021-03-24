---
title: "Creating Form Validations with React Hooks"
layout: post
date: 2020-01-03 22:48
image: /assets/images/markdown.jpg
headerImage: false
tag:
- React
- React Hooks
category: blog
author: prakhargupta
description: Creating Form Validations with React Hooks
---

# Creating Form Validations with React Hooks

## What are React Hooks and Why you should use them

In a nutshell, Hooks let you use React’s features without classes. They allow for functional components to have a state and utilize lifecycle methods. We do not need to rely on class components for that functionality. There are a variety of reasons for using hooks. One major reason is that stateful logic is hard to reuse between components. You can read more about this here https://reactjs.org/docs/hooks-intro.html. Also, they help in making the code more readable.

## Getting Started

Let’s use “create react app” to create our application. Type in Terminal:
    
    npx create-react-app react-hooks-form
    
Now you should enter the created folder and type:

    npm start
    
You should see something like this:

Now, Go to “src” folder and delete all files. Then create a file named ‘index.js’ and write the following Code in there:

    import React from 'react';
    import ReactDOM from 'react-dom';
    import Form from './Form';
    ReactDOM.render(
      <form>,
      document.getElementById('root')
    );
    </form>
    
This is just the bare bones of React. If you can’t understand it, you might want to take a step back and learn more about React before reading ahead.

Next, We will create the file Form.js, which will contain our form inside of it. Here’s what the initial code structure will look like:

    import React from 'react';
    const Form = () => {
        return (
          
            <div>
              <label>Email Address</label>
              <input type="email" name="email" required="">
            </div>
            <div>
              <label>Password</label>
              <input type="password" name="password" required="">
            </div>
            <button type="submit">Submit</button>
          
        )
    }
    export default Form;
We are making a form with email and passwords as the input fields, which we will validate later. Keep in mind that we have to use functional components instead of classes because hooks only work for functional components.

## Adding Basic Hooks:
Create a file called customHooks.js and add the following code in it. I’ll explain everything below.

    import React,{useState} from 'react';
    const useForm = (initialValues) => {
        const [inputs,setInputs] = useState(initialValues);
        const handleSubmit = (event) => {
          if(event){
            event.preventDefault();
          }
          console.log(inputs);
        }
        const handleInputChange = (event) => {
          event.persist();
          setInputs(inputs => ({...inputs, [event.target.name]: event.target.value}));
          }
        return {
          handleSubmit,
         handleInputChange,
         inputs
          };
    }
    export default useForm;
    
The ‘useState’ hook is used to initialize a state function and its setters. handleSubmit is invoked whenever the user clicks on the submit button. handleInputChange is invoked whenever any value is updated in email or password field. Finally, we return both functions as well as inputs state.

Next, we should update our Form component so that it uses our custom hook.

    import React from 'react';
    import useForm from './customHooks';
    const Form = () => {
        const {inputs, handleInputChange, handleSubmit} = useForm({email:'',password:''});
        return (
          <form onsubmit="{handleSubmit}">
            <div>
              <label>Email Address</label>
              <input type="email" name="email" onchange="{handleInputChange}" value="{inputs.email}" required="">
            </div>
            <div>
              <label>Password</label>
              <input type="password" name="password" onchange="{handleInputChange}" value="{inputs.password}" required="">
            </div>
            <button type="submit">Submit</button>
          </form>
        )
    }
    export default Form;
    
The line

    const {inputs, handleInputChange, handleSubmit} = useForm({email:'',password:''});
is used to provide the initial values.We will also use a callback function here later.

Now, we can see that by using hooks, we can avoid binding “this” which is difficult to understand.

## Validating the forms
Create a file named ‘validate.js’ where we will write our validation function. We should check that both email and passwords are entered, and that they are of correct expression.

     const validate = (inputs) => {
       //Email errors
      const errors = {};
      if (!inputs.email) {
          errors.email = 'Check Email';
      } else if (
          !/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i.test(inputs.email)
      ) {
          errors.email = 'Invalid email address';
      }
      //Password Errors
      if(!inputs.password  || inputs.password.length<6){
          errors.password = 'Check Password'
      }
      return errors;
    }
    export default validate;
    
The validate is a simple function that will take inputs as parameter and check and return any errors found.

Now we need to change our handleSubmit function so that it checks for errors before submitting the form. The submit function will look like this:

    const handleSubmit = (event) => {
        event.preventDefault();
        const validationErrors = validate(inputs);
        const noErrors = Object.keys(validationErrors).length === 0;
        setErrors(validationErrors);
        if(noErrors){
          console.log("Authenticated",inputs);
        }else{
          console.log("errors try again",validationErrors);
        }
    }
Also, we need to change the Form function to display any errors found.

    const Form = () => {
        const {inputs, handleInputChange, handleSubmit ,errors} = useForm({email:'',password:''},validate);
        return (
          <form onsubmit="{handleSubmit}">
            <div>
              <label>Email Address</label>
              <input type="email" name="email" onchange="{handleInputChange}" value="{inputs.email}" required="">
            </div>
            {errors.email && <p>errors.email</p>}
            <div>
              <label>Password</label>
              <input type="password" name="password" onchange="{handleInputChange}" value="{inputs.password}" required="">
            </div>
            {errors.password && <p>errors.password</p>}
            <button type="submit">Submit</button>
          </form>
        )
    }
    
That’s it!!!. Your app should validate the email and password before submitting the form and the results are shown in console. You can find the complete code for this tutorial here https://github.com/prakhar897/react-hooks-form

Mail me at prakhar897@gmail.com if you have any queries.
