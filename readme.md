# Angular

---This Readme is a WIP and without contribution it will not be finished.Tough I do hope it is of some use, And I am very happy to work with you towards a complete guide for newbies like myself---
This readme contains my own progress towards developping a webApp with Angular.
My journey was instigated by a BeCode exercise: Basic-Angular-Form.
More on this exercise will be in the exercise-readme.md since I would like to keep this readme to summarise what I learn about angular.

## What is Angular ?

- A component based-framework for building scalable web applicatrions
- A collection of well-integrated libraries that cover a wide variety of features
  - Routing
  - Form management
  - client-server communication
  - ...
- A suite of developer tools to help us develop
  [More info](https://angular.io/guide/what-is-angular)

---

## Speed course

- TypeScript based Framework
- Very powerfull CLI
- Application generator
  - Configures:
    - Routing
    - Testing Framework
    - Style PreProcessor
- Component based
  - **@Component** decorator turns TypeScript classes into components
    - Class properties are reactive **state**
      - When their values change their component will make the UI rerender with the updated data
        - This is called **reactive state**
      - These can be bound with the HTML using double curly brackets
        - `<p>{{ attribute }}</p>`
    - The classes methods can be called in the html by adding an event listener in braces and the method to trigger next to it - `<button (click)="doStuff()">Do!</button>`
    - (event)=binding;
- Angular has a variety of directives to build templates
  - Some very common ones
    - \*ngIf - Only render element when truthy
      - `<h1 *ngIf="angular===cool">Hello World!</h1>`
    - \*ngFor - Loop over itteratable value
      - `<p *ngFor="fruit in fruits">{{fruit}}</p>`
      - Angular rocks at handling complexity, making it simpler for the developer

---

## [Dependency Injection](https://angular.io/guide/dependency-injection)

- Share data between different components
- Done trough a **service**
  - can be recognised by **@Injectable** decorator
  - acts as a **global singleton**
  - State and logic can be used by any component.
    - The service is injected by adding the class to the constructor
      - `constructor(public objectname: ServiceName){}`

---

## [Angular Components](https://angular.io/guide/component-overview)

Components are the building blocks of any Angular application! So let's focus a bit more on these and how they work.

- What is a component ?

  - A controller for the UI.
  - Control the user experience
  - can be created with the Angular CLI
    - `ng generate component my-component`

- What is all this code in my component ?

  - @Component
    - Angular Spice!
    - Allows the binding of data between HTML and the component's class attributes
    - Contains the component's **selector**
      - This is the name we need to use the component within our html
        - `<component-name></component-name>`

- What are all these files ?

  - Every component consists of 4 files
    - TypeScript (holds the component's class)
    - CSS/SCSS/... (custom styling that does not bleed out of the component)
    - HTML (has the actual HTML of the component)
    - TestFile (have fun first, but this file will keep you from going insane once you work in a team)

- What is this data binding ?

  - Class attributes can be used within the HTML to create a **reactive state**

    - Examples:

      - This is the HTML for a disabled button without angular spice
        - `<button disabled>Click me!</button>`
      - Same button with angular spice

        - `<button [disabled]='attribute'>Click me!</button>`
        - Disabled is now bound to the component's class's attribute: attribute
        - Whenever the value of this attribute is true, the button will be disabled!

      - The same button with angular's spicy method biding
        - `<button [disabled]='attribute' (click)="handleClick()">click me</button>`
        - When this button is clicked a click event will trigger the class's _handleClick()_ method
        - `handleClick(){this.attribute=!this.attribute}`
          - If this is the method, the button will disable on click :D

- [Build in Routawhat ? (router)](https://angular.io/guide/routing-overview)

  - Components can be rendered within it's context by adding their _html like_ tag
    - `<component-name></component-name>`
  - But if everything eventually lives within the app component, how do I render different pages ? built in **router!**
    - This is supposed to be a speed course - tough honorable mention:
      - The router will render components based on a certain url path
      - Your project (if chosen to integrate the router) will have an _app-routing.module.ts_ file in it's src directory.
      - Here we can add routes to the Routes constant:
        - `const routes: Routes = [{path:'/mypage',component: myComponent}]`
        - Now the component is rendered by the router when the url goes to /mypage :D

- I want to load my components Dynamicly!
  - For example a popup or modal
  - This can be done with for example:
    - The AlertController from the ionic framework
  - Angular elements.
    - Allows you to use angular components outside of angular

## [Angular Directives](https://angular.io/guide/built-in-directives)

- The best one, yes it is! => **\*ngIf='truthy'**

  - Conditionally render something on the page
  - ```<div *ngIf='clicked'><h1>Hello User!</h1><p>Looking good today!</p></div>`
  - The whole div will only render if clicked is truthy

- Another one you cannot avoid => **\*ngFor='let item of items'**

  - Loop over an array of data
  - `<div *ngFor='item of items'><h1>Here is your item:</h1><p>{{item}}</p></div>`

  - The whole div will render for each item within the items array!

- I want to conditionally change my CSS! => **\*[ngClass]="{'classname': value === truthy, 'another-conditional-classname': anotherValue === truthy}"**;

  - Notice we pass in an object that has string attributes(your class names);
  - Their value is an expression that will decide wether the class is added, or not.

- Okay, okay... It's awesome! how do I make my own ?
  - `ng generate directive _name_`
  - Looks like a component, but there is no html or css!
  - Directives are **used as attributes** on html elements to change it's properties!
  - Within the class we can bind to the properties of it's HTML element host by using the **@HostBinding** decorator
    - Example: `@HostBinding('height') height = 420;`
    - Now every HTML element using this directive will have a height of 420 just like the attribute `height=200`;
  - The directive can also add event listeners to it's host by using the **@HostListener** decorator
    - Example: `@HostListener('mouseenter',['event'])onHover(event){this.height = 69}`
    - When the element using this directive is hovered it's height will shrink

---

## Angular Pipes

A pipe is a way to transform data for display. Simple functions used within template expressions that take an input value and return a transformed value.

- How do I make one ?

  - `ng generate pipe my-pipe`
  - now within our custom pipe found in my-pipe.pipe.ts under src/app we implement the transform method.
    - The value will represent the input, the return value will be the output of the pipe
  - Example: `` transform(value: string):string{return `${value} has gone trough my pipe`} ``
  - So what happens ?
    - `<p>I can see the {{componentAttribute}}!</p>` Will render as a normal paragraph with the value the attribute:
      - I can see the light!
    - `<p>I can see the {{componentAttribute|my-pipe}}!</p>` Will render as a normal paragraph, but our attribute's value is transformed by the pipe
      - I can see the light has gone trough my pipe!

- There's a lot of pipes built in, and available as custom libraries.

  - Angular is used a lot. a lot of the pipes you'll want to use are already written in code
  - [Check out this library for example](https://fknop.gitbook.io/angular-pipes/)
  - [Here's the link to their github repository](https://github.com/fknop/angular-pipes)
  - Or be adventurous and get started with them: `npm install angular-pipes --save`

- Really cool usecase: Async pipe
  - When code runs async a normal `*ngFor` loop may not work. since we need an array for this.
    - we can simply use the Async pipe which will kind of 'subscribe' to the data passed in.
    - Example: `<div *ngFor="let item of items | async"><p>hi I am {{item}}</div>`
    - the async pipe will convert the async data within items to an array and update the array when new data is added to items.
      - Simply: We fetch data in async. and the async pipe let's us use this data like a javascript array in our code!

---

## Lifecycles

These are implemented like interfaces - Example: `export class MyComponent implements OnInit{}`

- implements OnInit
  - Must have a method called **ngOnInit(){}**
  - What **code** do you want to **run** **when**ever this component is **initiated**
- implements OnDestroy
  - Must have a method called **ngOnDestroy()**
  - What **code** do you want to **run** **when**ever this component is **destroyed**
  - Remember this one to prevent performance issues or memory leaks.
- implements **AfterViewInit()**
  - Must have a method called **ngAfterViewInit()**
  - Your component might have some child views as well
  - What **code** do you want to **run** **when**ever this component's **childeren** are **loaded**
- implements **DoCheck**
  - Must have a method called **ngDoCheck()**
  - Detects wether change happend (this get's complicated but you gotta know it. don't worry we keep it easy)
  - WIthout technicality, let angular's magic update stuff when it changes.
  - Tough DoCheck is very **handy for debugging**
  - Any code in here will trigger whenever a change happens on the page.
  - Yes, this is the place to put all your lovely console.log(),console.error(),console.table() magic to make sure everything works as you want it to.

---

## Smart Components vs. Dumb Components

- Creating a tonne of components can end up in a big mess.
- A seperation of concerns and responsibility
  - The Solution: Split them up!
    - Smart Components
      - I will do stuff
      - Example:HomeComponent - I do stuff with item data
    - Dumb Components
      - I will show stuff
      - Example:ItemComponent - I show the item
  - Example:
    - `ng generate component item` -> Create a dumb item component
    - `<div *ngFor='let item of items'><app-item [item]="item"></app-item></div>` -> Our smart component loops over it's array of items and uses the dumb component to render the item.

---

## HashTagMeTwo - NO TOUCHING THE DOM!

This is just an important rule, you can do anythingn with a little javascript manipulating the DOM, don't.
Or do, but expect a deep rabbit hole of bugs.

## Must haves! - WIP

- [Angular Augury](https://augury.rangle.io);
  - THE browser extension to debug and profile Angular webApps.
- IDE Extensions - vsCode
  - [it's vscode! here's a pack of all the extensions you want for Angular](https://marketplace.visualstudio.com/items?itemName=johnpapa.angular-essentials)
    - This pack is created by [John Papa](https://www.johnpapa.net) who seems to be considered as a web development guru.

---

## Folder Structure - WIP

Once more, just diving into this will inevitabely turn this whole project into a mess of code, with perhaps a nice guiding readme, but still. code and projects should be as self explanitory as possible. This can only be done using structure. (as far as I know), so. let's look up some best practices about this.

- What are these files Angular gave me ?
  - [There's nice docs!](https://angular.io/guide/file-structure)
- Endless reading
  - So, I found [this](https://www.tektutorialshub.com/angular/angular-folder-structure-best-practices/#comments) nice looking guide on creating structure,....
  - But it requires me to know about [Angular Modules](https://www.tektutorialshub.com/angular/angular-modules/)
  - Which to understand needs knowledge about more and more and more things....
- Time to skip a lot of reading, get out of tutorial hell, summarise,implement,
  - Aaand probably break a lot of stuff....
    - It'll be worth it!

### Angular Modules - WIP

Angular will not make distinction between modules, exactly what I want. Structure in my development area. tough unity in the production environment.
Tough according to the article modules can be split up into four main categories

- Root Module
  - The root of our project, what is loaded whenever its starts
  - This module is responsible for loading all the other modules
  - Is usually called AppModule and created in /src/app
- Features Module
  - A module that implements specific features in the application
  - All components,pipes and directives related to the feature will reside here.
  - Must be in a folder with the Module's name in /src/app/nameOfModule
- Shared Module
  - Some components,directives and pipes may be used across modules. this module will hold those pieces of code.
  - Services are not part of this module! Shared will be imported everywhere, and loading services where we don't use them may result in conflicts
  - This module should have NO DEPENDENCIES from other modules.
  - This module does for example
    - Import angular modules to then share to other modules
    - Import third party modules to share to other modules
- Core Module
  - Services shared across the application will reside here
    - Seperate module so that ensuring every service stays a singleton becomes easier
  - Services do for example:
    - Authentication services
    - Fetching data
  - This module must only be imported into the root module.
    - We can prevent other modules importing it with following code

```ts
@NgModule({})
export class CoreModule {
  constructor(@Optional() @SkipSelf() core: CoreModule) {
    if (core) {
      throw new Error(
        "You just wrote a book silly! don't import the core module outside of the root module!"
      );
    }
  }
}
```

- Thankfully within this module we can make dedicated folders for every service
  Unfortunately the article I am reading is pretty extensive and does not keep it's beginner friendly tone. so this is where I end this chapter for now. While I try to implement some structure in my project
