# Awesome Stepper Form with HTML/CSS/JavaScript
![stepper-form](https://drive.google.com/uc?id=1VdfNHyzdy8JkElzv8bgYYiWLu97QMtnB)

Stepper form is a great and useful feature regarding user experience, especially if you have long form.In this post, I will create a cool stepper form with HTML, CSS and JavaScript.
You can check it live on [Codepen](https://codepen.io/ibrahima92) : [Stepper Form](https://codepen.io/ibrahima92/full/bGGrVxq)

## 1. HTML
As you can see, the HTML file is relatively simple with several classes i might say.
```
    <main>
      <div class="stepper">
        <div class="step--1 step-active">Step 1</div>
        <div class="step--2">Step 2</div>
        <div class="step--3">Step 3</div>
        <div class="step--4">Finish</div>
      </div>
      <form class="form form-active">
        <div class="form--header-container">
          <h1 class="form--header-title">
            Personal Info
          </h1>

          <p class="form--header-text">
            Tell us more about you.
          </p>
        </div>
        <input type="text" placeholder="Name" />
        <input type="text" placeholder="Email" />
        <input type="text" placeholder="Password" />
        <button class="form__btn" id="btn-1">Next</button>
      </form>
      <form class="form">
        <div class="form--header-container">
          <h1 class="form--header-title">
            Company Info
          </h1>

          <p class="form--header-text">
            Tell us more about your company.
          </p>
        </div>

        <input type="text" placeholder="Company Name" />
        <input type="text" placeholder="Job title" />
        <input type="text" placeholder="Location" />
        <button class="form__btn" id="btn-2-prev">Previous</button>
        <button class="form__btn" id="btn-2-next">Next</button>
      </form>
      <form class="form">
        <div class="form--header-container">
          <h1 class="form--header-title">
            Social account
          </h1>

          <p class="form--header-text">
            Tell us more about your social account.
          </p>
        </div>
        <input type="text" placeholder="Linkedin" />
        <input type="text" placeholder="Twitter" />
        <input type="text" placeholder="Github" />
        <button class="form__btn" id="btn-3">Submit</button>
      </form>
      <div class="form--message"></div>
    </main>
```
Beside the **main** tag, i firstly define a **div** that hold the stepper element. Then we have three **forms** with different button **id** that will enable soon the stepper effect with JavaScript.

## 2. CSS
We begin with some resets and set *font-familly* and *background-color* for the **body** tag. 
```
@import url('https://fonts.googleapis.com/css?family=Nunito&display=swap');
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  background: #f5f6f7;
  font-family: 'Nunito', sans-serif;
}

main {
  height: 100vh;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  position: relative;
}
```
Then for the **main** tag, we use *flex* to literally center the element relatively for the **body** tag with the help of *justify-content* and *align-items* properties.
```
.stepper {
  width: 20rem;
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: 5%;
}

.step--1,
.step--2,
.step--3,
.step--4 {
  width: 5rem;
  padding: 0.5rem 0;
  background: #fff;
  color: #666;
  text-align: center;
}
.step--1,
.step--2,
.step--3 {
  border-right: 1px solid #666;
}
```
For the Stepper element, we use again *flex* to align horizontally the four steps. Then use each step class to add some nice style. For the Stepper element, we use again *flex* to align horizontally the four steps. Then use each step class to add some nice style.
```
.form {
  background: #fff;
  text-align: center;
  position: absolute;
  width: 25rem;
  box-shadow: 0.2rem 0.2rem 0.5rem rgba(51, 51, 51, 0.2);
  display: none;
  border-radius: 1rem;
  overflow: hidden;
}
.form--header-container {
  background: linear-gradient(to right, rgb(51, 51, 51), #919191);
  color: #fff;
  height: 6rem;
  padding: 1rem 0;
  margin-bottom: 2rem;
}

.form--header-title {
  font-size: 1.4rem;
}

.form--header-text {
  padding: 0.5rem 0;
}

input[type='text'] {
  padding: 0.8rem;
  margin: auto;
  margin-top: 0.5rem;
  width: 20rem;
  display: block;
  border-radius: 0.5rem;
  outline: none;
  border: 1px solid #bdbdbb;
}

.form__btn {
  background: #333;
  color: #fff;
  outline: none;
  border: none;
  padding: 0.5rem 0.7rem;
  width: 7rem;
  margin: 1rem auto;
  border-radius: 0.9rem;
  text-transform: uppercase;
  font-weight: 700;
  cursor: pointer;
}
.form--message-text {
  width: 25rem;
  background: #fff;
  color: #444;
  padding: 2rem 1rem;
  text-align: center;
  font-size: 1.4rem;
  box-shadow: 0.2rem 0.2rem 0.5rem rgba(51, 51, 51, 0.2);
  animation: fadeIn 0.8s;
  border-radius: 1rem;
}
``` 
We have three forms element in the HTML file, that's the reason why we use *position: absolute* to superpose them. At the beginning, we will hide all three forms and only the form with the **active class** will be shown.
On the **form--header-container** class we use *linear-gradient* to add some nice style to the form header.
Then, on the **form--message-text** class, we add the *animation* property to have a cool fade in effect when the success message will show.
```
.form-active {
  z-index: 1000;
  display: block;
}
.form-active-animate {
  animation: moveRight 1s;
}
.form-inactive {
  display: block;
  animation: moveLeft 1s;
}

.step-active {
  background: #666;
  color: #fff;
  border: 1px solid #666;
}
```
 All three forms will be hidden at the beginning. Therefore, we use **form-active** class to show the current form and also *z-index* property to be sure that the chosen form will be always at the top.
Then the **form-active-animate** class will make a cool animation entrance from the left to the right.
We also have a **form-inactive** class that will help us hiding the previous form. And the **step-active** will just change the current step element style.
```
@keyframes moveRight {
  0% {
    transform: translateX(-27rem) scale(0.9);
    opacity: 0;
  }
  100% {
    transform: translateX(0rem) scale(1);
    opacity: 1;
  }
}

@keyframes moveLeft {
  0% {
    transform: translateX(0rem) scale(1);
    opacity: 1;
  }
  100% {
    transform: translateX(27rem) scale(0.9);
    opacity: 0;
  }
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
```
As you can see here, we use **keyframes** to do three animations. The first animation *moveRight* will literally move the element from the left to the right with the *transform* property and the *translateX and scale values*.For the second animation *moveLeft*, this is the same process except the fact that the element will move more on the right side. And for the last animation *fadeIn*, it will enable the fade in effect when the element will show.
## 3. JavaScript
```
const formBtn1 = document.querySelector('#btn-1');
const formBtnPrev2 = document.querySelector('#btn-2-prev');
const formBtnNext2 = document.querySelector('#btn-2-next');
const formBtn3 = document.querySelector('#btn-3');
```
To interact with the DOM, we need to select all form buttons with the help of *querySelector*.
```
// Button listener of form 1
formBtn1.addEventListener('click', function(e) {
  gotoNextForm(formBtn1, formBtnNext2, 1, 2);
  e.preventDefault();
});

// Next button listener of form 2
formBtnNext2.addEventListener('click', function(e) {
  gotoNextForm(formBtnNext2, formBtn3, 2, 3);
  e.preventDefault();
});

// Previous button listener of form 2
formBtnPrev2.addEventListener('click', function(e) {
  gotoNextForm(formBtnNext2, formBtn1, 2, 1);
  e.preventDefault();
});

// Button listener of form 3
formBtn3.addEventListener('click', function(e) {
  document.querySelector(`.step--3`).classList.remove('step-active');
  document.querySelector(`.step--4`).classList.add('step-active');
  formBtn3.parentElement.style.display = 'none';
  document.querySelector('.form--message').innerHTML = `
   <h1 class="form--message-text">Your account is successfully created </h1>
   `;
  e.preventDefault();
});
```
As you can see here, we listen to, click event and apply the *gotoNextForm* function by passing the previous form, the next form, the previous step and the next step as parameters and by the way use *preventDefault () * on the event to prevent page reload.
For the *formBtn3* listener, this is a little bit different because we show a success message to the user by using *innerHTML* to add the message on the empty **div** with the class of **form--message**
```
const gotoNextForm = (prev, next, stepPrev, stepNext) => {
  // Get form through the button
  const prevForm = prev.parentElement;
  const nextForm = next.parentElement;
  const nextStep = document.querySelector(`.step--${stepNext}`);
  const prevStep = document.querySelector(`.step--${stepPrev}`);
  // Add active/inactive classes to both previous and next form
  nextForm.classList.add('form-active');
  nextForm.classList.add('form-active-animate');
  prevForm.classList.add('form-inactive');
  // Change the active step element
  prevStep.classList.remove('step-active');
  nextStep.classList.add('step-active');
  // Remove active/inactive classes to both previous an next form
  setTimeout(() => {
    prevForm.classList.remove('form-active');
    prevForm.classList.remove('form-inactive');
    nextForm.classList.remove('form-active-animate');
  }, 1000);
};
```
The *gotoNextForm* function will receive four parameters. Then, we traverse the DOM with *parentElement* on both prevForm and nextForm variables to reach the **form** element.
And we use nextStep and prevStep variables to select the previous and next steps on the stepper element.
After selecting elements, we add the **form-active** class to the next form element and **form-active-animate** class to have some nice animation.
Then, we add **form-inactive** class to the previous form.
After that, We use the same process for the stepper element. By adding the **step-active** class to the next step and remove it from the previous step.
And finally remove **form-active**, **form-inactive** and **form-active-animate** classes to both previous and next form after 1 second with setTimeout().

And We finally get our Awesome Stepper Form with HTML, CSS and JavaScript. You can also check my other pens [here](https://codepen.io/ibrahima92) or follow me on [Twitter](https://codepen.io/ibrahima92).
That's all folks!
Happy Coding...
