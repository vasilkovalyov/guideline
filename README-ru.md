# Советы по созданию проектов &middot; [![ПРы приветствуются](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

<hr>

- [Git](#git)
  - [Правила работы с Git](#some-git-rules) 
  - [Пишем хорошее сообщение коммита](#writing-good-commit-messages)
- [Структура и Именование](#structure-and-naming)
- [Оформление кода](#code-style)
  - [Советы по оформлению кода](#code-style-check)
    - [Структура react component](#react-component-structure)
    - [Markup struct for section(block)](#markup-struct-for-section)
    - [Styles](#styles)
  


<a name="git"></a>

## 1. Git

![Git](/images/branching.png)

<a name="some-git-rules"></a>

### 1.1 Правила работы с Git

Набор правил, которые следует иметь ввиду:

- Откалывайте ветку от `main`

- Разрабатывайте в `feature/*` ветке.
- Фиксите в `fix/*` ветке.
- Рефакторите в `refactoring/*` ветке.


- Никогда не выкладывайте (push) коммиты напрямую в  `main` ветку. Создавайте Запрос на Слияние (Pull Request).

- Обновляйте вашу локальную `main` ветку и делайте "rebase" перед тем как делать "push" своих изменений перед созданием pull request.

- Перед созданием "Pull Request" убедитесь, что ваша `feature/*` || `fix/*` || `refactoring/*` ветка успешно собирается и все тесты проходят успешно, включая проверки на оформление кода.


<a name="writing-good-commit-messages"></a>

### 1.2 Пишем хорошее сообщение коммита

Хороший гайдлайн по создании коммитов и следование ему облегчит работу с Git и сотрудничество с другими разработчиками. Вот несколько правил большого пальца ([источник](https://chris.beams.io/posts/git-commit/#seven-rules)):

- Начните краткое описание с заглавной буквы.

- Не заканчивайте краткое описание точкой.

- Используйте основное описание, чтобы объяснить **что** и **почему** вместо **как**.

<a name="structure-and-naming"></a>

## 2. Структура и Именование

![Структура и Именование](/images/folder-tree.png)

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



<a name="code-style"></a>

## 3. Оформление кода

![Оформление кода](/images/code-style.png)

<a name="code-style-check"></a>

### 3.1 Советы по оформлению кода

- Используйте `.eslintignore`, чтобы исключить файлы и папки из проверки на оформление кода.

- Избегайте неуместных и шуточных комментариев, логов и наименований.

- Используйте имена со смыслом, не сокращайте их, чтобы потом было легко их искать. Для функций используйте длинные и наглядные имена. Имя функции должно быть глаголом или глагольной фразой, и должно сообщать нам что делает функция.

- Располагайте функции в файле в соответствии с правилом понижения (step-down rule). Сложные составные функции располагаются в начале файла, а затем идут простые функции.


<a name="enforcing-code-style-standards"></a>

### 3.2 Обеспечение определенного стиля кода в react app

<a name="react-component-structure"></a>

#### 3.2.1 Структура React component

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




