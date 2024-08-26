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
  |   └── store - общий store для приложения
  ├── entities
  |   └── entity1
  |       └── api
  |       └── model
  ├── features
  |   └── feature1
  |   └── feature2
  ├── hooks - кастомные хуки
  |   └── useHook1
  |   └── useHook2
  ├── i18n - локализация для проекта
  |   └── locales
  |       └── en
  |       └── uk
  ├── layouts - шаблоны для страниц, как правило может быть для public pages, private pages
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
  |   └── base.scss - общие базовые стили
  |   └── breakpoints.scss - переменные для медиазапросов
  |   └── fonts.scss - для подключение шрифтов
  |   └── main.scss - собирает все scss файлы для общей компиляции
  |   └── variables.scss - переменные которые используются по всему проекту
  ├── widgets - 
  |   └── widget1
  |   └── widget2
  ```


- Структурируйте ваши файлы вокруг продуктовых функций / страниц / компонентов, а не ролей. Также размещайте файлы с тестами рядом с файлами, к которым они относятся.

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


- Именование для pages

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
  
- Именование для hooks

  ```
  .
  ├── hooks
  |   └── useHook.tsx
  ```
  
- Именование для components, features, widgets

  ```
  .
  ├── [folder]
  |   └── component-name
  |       └── index.ts
  |       └── componentName.tsx
  ```

  _Why:_

  > Вместо длинных списков файлов вы получите небольшие модули, которые инкапсулируют только одну обязанность и включают в себя  связанные файлы. Навигация в проекте станет гораздо легче, так как нужные файлы будут находиться рядом, сгруппированные по модулям.



<a name="code-design"></a>

## 3. Code design

![Оформление кода](/images/code-style.png)

<a name="code-formatting-tips"></a>

### 3.1 Code Formatting Tips

- Используйте `.eslintignore`, чтобы исключить файлы и папки из проверки на оформление кода.

- Избегайте неуместных и шуточных комментариев, логов и наименований.

- Используйте имена со смыслом, не сокращайте их, чтобы потом было легко их искать. Для функций используйте длинные и наглядные имена. Имя функции должно быть глаголом или глагольной фразой, и должно сообщать нам что делает функция.

- Располагайте функции в файле в соответствии с правилом понижения (step-down rule). Сложные составные функции располагаются в начале файла, а затем идут простые функции.


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




