# Tips for creating projects &middot; [![ПРы приветствуются](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

<hr>

- [Git](#git)
  - [Rules for working with Git](#some-git-rules) 
  - [Writing a good commit message](#writing-good-commit-messages)
- [Structure and Naming](#structure-and-naming)
- [Code design](#code-design)
  - [Code Formatting Tips](#code-formatting-tips)
    - [React component structure](#react-component-structure)
    - [Markup struct for section(block)](#markup-struct-for-section)
    - [Styles](#styles)
  


<a name="git"></a>

## 1. Git

![Git](/images/branching.png)

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

![Structure and Naming](/images/folder-tree.png)

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

![Code design](/images/code-style.png)

<a name="code-formatting-tips"></a>

### 3.1 Code Formatting Tips

- Use `.eslintignore` to exclude files or folders from code style checks.

- Avoid irrelevant or funny comments, logs or naming.

- Make your names search-able with meaningful distinctions avoid shortened names. For functions use long, descriptive names. A function name should be a verb or a verb phrase, and it needs to communicate its intention.

- Organize your functions in a file according to the step-down rule. Higher level functions should be on top and lower levels below.


<a name="enforcing-code-style-standards"></a>

### 3.2 Обеспечение определенного стиля кода в react app

<a name="react-component-structure"></a>

#### 3.2.1 React component structure

  - каждый компонент должен находится в папке, так же там должен быть index.ts файл откуда будут экспортироваться компоненты, типы и
    т.д для работы извне, ничего лишнего не стоит экспортировать
  - пример index.ts файла

```jsx
export { default as Card } from './Card.tsx'
```

  - third party libs
  - ui components
  - local components, use alias for import component e.g `src/widgets/component`
  - utils, use alias for import e.g `src/shared/themes/colors`
  - styles
  - types, interfaces типы для компонентов создаются внутри компоненты с окончанием Props e.g `interface CardProps {}`
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

- стили должны писаться или в scss или в на самих ui компонентах, если стилевых атрибов больше чем 4 или 5 и это выглядит громоздко то лучше перенести стили в .scss файл
- стили для Grid компонентов могут быть чуть больше чем 4 или 5 атрибутов, но стили должны быть для свойств flex, margin, padding, для более сложных стилей лучше создать класс и перенести стили в отдельный файл
- если есть практические одинаковые компоненты, секции по своему внешнему виду но возможно с чуть разной структурой лучше выносить стили в папку `styles/section` или `styles/component`
  


<a name="markup-struct-for-section"></a>

#### 3.2.2 Markup struct for section(block)

- название секции должно начинаться с Section

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

- стили пишутся по BEM

```
  .card { // block
    &--active {} // modificator
    &__title {} // element
    &__description {} // element
  }
```

- важно писать цвета как var переменные

  ```
    .card {
      background-color: rgb(var(--primary-color));
    }
  ```
  
- для медиазапросов в рядом с tsx компонентами нужно использовать переменные таким образом

  ```
    @use "styles/breakpoints.scss" as breakpoints;
   
    .card {
      background-color: rgb(var(--primary-color));
    }
  ```
  
- для медиазапросов в файлах папки `styles` нужно использовать переменные таким образом

  ```
    @use "path-to-file/breakpoints.scss" as breakpoints;
   
    .card {
      background-color: rgb(var(--primary-color));
    }
  ```




