# Советы по созданию проектов &middot; [![ПРы приветствуются](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

<hr>

- [Git](#git)
  - [Правила работы с Git](#some-git-rules)
  - [Рабочий процесс в Git](#git-workflow)
  - [Пишем хорошее сообщение коммита](#writing-good-commit-messages)
- [Структура и Именование](#structure-and-naming)
- [Оформление кода](#code-style)
  - [Советы по оформлению кода](#code-style-check)
    - [Структура react component](#react-component-structure)
  - [Обеспечение определенного стиля кода](#enforcing-code-style-standards)
- [API](#api)
  - [Дизайн API](#api-design)
  - [Безопасность API](#api-security)
  - [Документация API](#api-documentation)
- [Лицензирование](#licensing)

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


  > Коммиты должны быть краткими и максимально сфокусированными; это не место для многословия. [узнать больше...](https://medium.com/@preslavrachev/what-s-with-the-50-72-rule-8a906f61f09c)

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

  **Плохо**

  ```
  .
  ├── productCard
  |   └── productCard.ts
  ├── banner
  |   └── banner.tsx
  ```

  **Хорошо**

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

  _Почему:_

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

  - third party libs
  - ui components
  - local components, use alias for import component e.g `src/widgets/component`
  - utils, use alias for import e.g `src/shared/themes/colors`
  - styles
  - types, interfaces типы для компонентов создаются внутри компоненты с окончанием Props e.g `interface CardProps {}`
  - render component
   
```jsx
import React from 'react'
import cn from 'classnames'

import { Box, Button } from "@mui/material";

import LocalComponent from 'src/widgets'

import './Card.scss'

interface CardProps {
    title: string,
    description: string,
    className?: string
}

const Card = ({ title, description, className }: CardProps) => {
    return (
      <Box className={'card', className}>
        <Typography>{title}</Typography>
        <Typography>{description}</Typography>
      </Box>
    )
}

export default Card;
```
  
  

### 3.3 Обеспечение определенного стиля кода в styles


