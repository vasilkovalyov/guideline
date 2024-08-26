# Tips for creating projects &middot; [![ПРы приветствуются](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

<hr>

- [Git](#git)
  - [Rules for working with Git](#some-git-rules) 
  - [Writing a good commit message](#writing-good-commit-messages)
- [Structure and Naming](#structure-and-naming)
- [Code design](#code-design)
  - [Code Formatting Tips](#code-formatting-tips)
  - [Enforcing code style standards](#enforcing-code-style-standards)
    - [React component structure](#react-component-structure)
    - [Markup struct for section(block)](#markup-struct-for-section)
    - [Styles](#styles)
  

<a name="git"></a>

## 1. Git


<a name="some-git-rules"></a>

### 1.1 Rules for working with Git

A set of rules to keep in mind:

- Created branch from `main`

- Develop in `feature/*` branch.
- Fix issues in `fix/*` branch.
- Refactoring in `refactoring/*` branch.


- Never push commits into  `main` branch directly. Make Pull Request.

- Update your local `main` branch and do an interactive rebase before pushing your feature and making a Pull Request

- Before making a Pull Request, make sure your branch builds successfully and passes all tests (including code style checks).


<a name="writing-good-commit-messages"></a>

### 1.2 Writing a good commit message

Having a good guideline for creating commits and sticking to it makes working with Git and collaborating with others a lot easier. Here are some rules of thumb (source): ([источник](https://chris.beams.io/posts/git-commit/#seven-rules)):

- Capitalize the subject line.

- Do not end the subject line with a period.

- Use imperative mood in the subject line.


<a name="structure-and-naming"></a>

## 2. Structure and Naming


```
  .
  ├── app
  |   └── api
  |   └── routing
  |   └── store - base store for the app
  ├── entities
  |   └── entity1
  |       └── api
  |       └── model
  ├── features
  |   └── feature1
  |   └── feature2
  ├── hooks - custom hooks
  |   └── useHook1
  |   └── useHook2
  ├── i18n - localization for the projects
  |   └── locales
  |       └── en
  |       └── uk
  ├── layouts - layouts for pages can have unique header, footer, as a rule there are public, private type of layouts
  |   └── PrivateLayout
  |   └── PublicLayout2
  ├── pages
  |   └── Page1
  |   └── Page2
  ├── shared
  |   └── api
  |   └── config
  |   └── themes
  ├── styles
  |   └── components
  |       └── component1
  |       └── component2
  |   └── sections
  |       └── section1
  |       └── section2
  |   └── base.scss - common base styles
  |   └── breakpoints.scss - variable only for breakpoints
  |   └── fonts.scss - for import fonts
  |   └── main.scss - consist of styles (components, section, etc) except for variables
  |   └── variables.scss - variable that use in entire app
  ├── widgets - 
  |   └── widget1
  |   └── widget2
  ```


- How you have to create components

  **Bad**

  ```
  .
  ├── productCard
  |   └── productCard.ts
  ├── banner
  |   └── banner.tsx
  ```

  **Good**

  ```
  .
  ├── product-card
  |   ├── index.ts
  |   └── productCard.tsx

  ├── banner
  |   ├── index.ts
  |   ├── banner.tsx
  ```


- Naming for pages

  ```
  .
  ├── pages
  |   └── home
  |       └── index.ts
  |       └── Home.tsx
  |   └── create-course
  |       └── index.ts
  |       └── CreateCourse.tsx
  ```
  
- Naming for hooks

  ```
  .
  ├── hooks
  |   └── useHook.tsx
  ```
  
- Naming for components, features, widgets

  ```
  .
  ├── [folder]
  |   └── component-name
  |       └── index.ts
  |       └── componentName.tsx
  ```

  _Why:_

  > Instead of a long list of files, you will create small modules that encapsulate one responsibility including its test and so on. It gets much easier to navigate through and things can be found at a glance.


<a name="code-design"></a>

## 3. Code design


<a name="code-formatting-tips"></a>

### 3.1 Code Formatting Tips

- Use `.eslintignore` to exclude files or folders from code style checks.

- Avoid irrelevant or funny comments, logs or naming.

- Make your names search-able with meaningful distinctions avoid shortened names. For functions use long, descriptive names. A function name should be a verb or a verb phrase, and it needs to communicate its intention.

- Organize your functions in a file according to the step-down rule. Higher level functions should be on top and lower levels below.


<a name="enforcing-code-style-standards"></a>

### 3.2 Enforcing code style standards

<a name="react-component-structure"></a>

#### 3.2.1 React component structure

  - every single component should has a folder itself, there is should be `index.ts` where you can export component, types etc for work outside of the folder, you shouldn`t export useless files or types.
  - expample `index.ts`

```jsx
export { default as Card } from './Card.tsx'
```

  - third party libs
  - ui components
  - local components, use alias for import component e.g `src/widgets/component`
  - utils, use alias for import e.g `src/shared/themes/colors`
  - styles
  - types, interfaces - types for component create with ending - `Props` e.g `interface CardProps {}`
  - render component
  

```jsx
import { FC } from "react";
import cn from 'classnames'

import { Box, Button } from "@mui/material";

import LocalComponent from 'src/widgets'

import './Card.scss'

interface CardProps {
    title: string,
    description: string,
    className?: string
}

const Card: FC<LandingHeroSectionProps> = ({
  title, description, className
}) => {
    return (
      <Box className={"card", className}>
        <Typography className="card__title">{title}</Typography>
        <Typography className="card__description">{description}</Typography>
      </Box>
    )
}

export default Card;
```

- in mui components you have you write values only in `px` e.g

**Bad**  
```jsx
<Box pt={5}></Box>
```

**Good**
```jsx
<Box pt="40px"></Box>
```
  
- you have to write styles insde folder with the components or inside `styles` folder or on the ui components
- if you put style attributes for ui components you need to limit them till 4 or 5 attributes, otherwise it will looks cumbersome and you should put styles into `.scss` file
- styles for Grid, Stack, List components can use more that 4,5 attributes, however thay should be for styles `flex, padding, margin` otherwise you have to create separate `.scss` file for the component and write styles there
- if you have almost similar components, or sections that looks same with different structure you can try to create `.scss` file for the component and put it into `styles/components` or `styles/sections` and don't forget import file into  `index.scss` for folder it exist for

  


<a name="markup-struct-for-section"></a>

#### 3.2.2 Markup struct for section(block)

- naming of section should start with `Section`

```jsx
import React from 'react'

import { Box, Container } from "@mui/material";

import './SectionAbout.scss'


const SectionAbout = () => {
    return (
      <Box component="section" className="section-about">
        <Container>
          /* content */
        </Container>
      </Box>
    )
}

export default SectionAbout;
```

<a name="styles"></a>

#### 3.2.3 Styles

- we use BEM for classnames

```
  .card { // block
    &--active {} // modificator
    &__title {} // element
    &__description {} // element
  }
```

- it is essential write variable for colors

  ```
    .card {
      background-color: rgb(var(--primary-color));
    }
  ```
  
- breakpoints inside the component folders inside `.scss` files you have to write like that

  ```
    @use "styles/breakpoints.scss" as breakpoints;
   
    .card {
      background-color: rgb(var(--primary-color));
    }
  ```
  
- breakpoints inside `styles` you have to write like that

  ```
    @use "path-to-file/breakpoints.scss" as breakpoints;
   
    .card {
      background-color: rgb(var(--primary-color));
    }
  ```

- line-height you have to write in `em` e.g `line-height: 1.2;`
- we use mobile first responsive
  
- for transition you have to use mixin `animate`
  
```
    @use "path-to-file/mixins.scss" as mixins
   
    .card {
      @include animate(background-color color) 
    }
```

- for media query you have to use mixin `media`
  
```
    @use "path-to-file/mixins.scss" as mixins
   
    .card {
      @include mixins.media(tablet) {
        border: none;
      }
    }
```

- for hover effect you have to use mixin `hover` it works only for screen without touch
  
```
    @use "path-to-file/mixins.scss" as mixins
   
    .card {
      @include mixins.hover {
        border: none;
      }
    }
```

