# Ignore this readme, I'll just blindly follow the step by step guide.

I can't write a structured readme without an understanding of a structured project.
Everything is either guesswork or 2-4 hours of guesswork. I'm over 20 hours into this project and haven't gotten a hello world!

## Friend-List

A basic webapp that shows a form where people can enter their information to add themselves to your friendlist

## Learning Objectives

- Use of the Angular CLI
- Improve your understanding of TypeScript
- Basic understanding of Angular
  - Components
  - Services
- Configure a NodeJS API
- Creation of an Angular form
- Communicate between a NodeJS server and an Angular APP

## Must Haves

- The Form fields:
  - First name - Text input
  - Last Name - Text input
  - Email - Text input
  - Phone number - Text input
  - Favourite Programming language - Selectable provided options
- Visual feedback on the user input.
- Form validation
- A representation of the friends
  - The exercise requires us to do this trough a GET request.
- A way to add the form's information to the friend list
  - The exercise requires us to do this trough a POST request.

## Nice To Haves:

- Form validation (again?)
  - Make sure the phone number is a real phone number
    - Here it's ok to be country specific.
- Seperate pages
  - One to add a friend
  - One to see the friendlist
- Best friend's list
- Some extra data fields.
- Custom getters.
  - Examples:
    - Only show the friends that like PHP
    - A list of people between age x and x
    - .... Go crazy

## My Roadmap to the end of this exercise:

- Getting what I need:
  - TypeScript
    - `brew install typescript`;
  - Angular CLI
    - `brew install angular-cli`;
    - `ng version`;
    - don't enable autocomplete since it has bugs.(and writes to my home directory without telling me what.)
    - Nope, I am happy to share some data to improve Angular. But there is no way that data is Anonymous.
    - Yay, we get some cool ASSCI pattern welcoming us.
  - Node v16.x.x LTS
    - `brew install node@16`;
    - `echo 'export PATH="/opt/homebrew/opt/node@16/bin:$PATH"' >> ~/.zshrc`
  - some IDE extensions
    - I picked some from [this](https://marketplace.visualstudio.com/items?itemName=johnpapa.angular-essentials) pack

### Have a basic understanding of angular

- All the knownledge I have/Find on angular will be posted in this repository's readme.md
- Currently still adding source links, but I want to get back to coding this project ASAP!

### Getting started - No more tutorial hell

Thankfully my coach Tim provided a step by step guide that guides us trough all of the necessary steps to create this project!
However....... I want to know what's going on. So I will follow along. But I won't let you drag me forward.
Since at this moment I don't have anythign, I guess it's time to start by just creating the front end before trying to implement a server side part.

### Creating the webApp

This CLI is so op....

```shell
cd ~/Web/BeCode/Angular/friend-book;
ng new friend-book;
```

Since the exercise says to use two pages, I say yes to the routing.
I really want to use Tailwind here, but I think plain CSS is a better way to get used to Angular, and component based development for now.
Sip some coffeee............
.....
.....

`✔ Packages installed successfully. Directory is already under version control. Skipping initialization of git. `

```shell
cd friend-book;
ng serve --open;
```

Nice! Let's get started.

- `Exercise says:Delete stuff!`
  Time to take some notes first on what we get!
- [x] Add the [Angular Tutorial](https://angular.io/tutorial) to my endless TODO list of tutorials. √
- [x] Bookmark the [CLI documentation](https://angular.io/cli) √
- [x] Bookmark this interesting link to [Angular Material](https://material.angular.io) √

Yeet-time!

- Empty everything in the app.component.html
  - ! Except for <router-outlet></router-outlet>
- Empty out the App Component class in the app.component.ts
- Fix the error in the testfile app.component.spec.ts

Done! Let's get coding!

### Layout

What I know:

- I will eventually need more than one page to succeed in this project
- I want some kind of navigation between these
- I want to keep my code organised
  What I'll do with this information:
- Create a folder structure within the app
  - [Gotta love the internet](https://www.tektutorialshub.com/angular/angular-folder-structure-best-practices/)
  - Let's create this folder structure keeping in mind what i'm creating.
  - I will try to document this under Folder structure in the general readme

### Create the form

With my new found understanding, this is the first stubborn deviation I will make of the instructions. I will still try to follow the guiding hand as much as possible. But I just learned I should be developing with components! I need a form so time to create a component for it.
I'll probably need a couple, since I know in the future I want different pages on the app. And I want to try use the smart-dumb component principle.

- The tutorial tells me to import magic from angular.... Since I do not know how to cast spells, time to open up [this documentation](https://angular.io/guide/forms) on the side.

Ok, let's make a mess....
In a way that makes sense to me, so I'm setting aside this theory for now

Let's make following structure and figure it out

- src/app/pages/
  - Contains every single one of 3 pages
    - Foes
      - Overview of everyone who did not want to become friends
    - Friends
      - Overview of awesome people
    - Become related
      - The form itself
- src/app/components
  - Contains all components i'll be creating for this app
