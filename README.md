# React-TypeScript-Code-Styles

## React Styling

There are several ways to style components in React. From ideal to less-ideal, here are some of the more popular methods:

1. Styled Components
1. React CSS Properties
1. Stylesheet (CSS or SCSS)

## Styled Components

[Styled components](https://emotion.sh/docs/styled) provides syntactic sugar for styling React components in a syntax similar to CSS. While it can be used for CSS nesting (similar to SCSS / Sass), the two big winners for using it are:

1. React Component Composition, and
1. Computed Styling


Here's a basic outline for creating a styled component:


```ts
// components/button/styled-components.ts

import styled from '@emotion/styled';

export const ButtonWrapper = styled.button`
  padding: 1rem 2rem;
  color: blue;
  background: white;
`;
```

```ts
// components/button/index.tsx

import * as React from 'react';
import * as S from './styled-components';


interface IButtonProps {
  children?: any
  onClick?: () => void
}

export const Button = (props: IButtonProps) => {
  return (
    <S.ButtonWrapper {...props}>
      {props.children}
    </S.ButtonWrapper>
  );
};
```

The styled components reside in a sibling file (`components/button/styled-components.ts`) to the exported component (`components/button/index.tsx`) so that we can separate our styling from our view.


### Styled Components Composition


Let's say we want to create a button for a new view that relies on the base styles of our basic button, but makes the text bolder.


```ts
// components/bold-button/styled-components.ts

import styled from '@emotion/styled';
import { ButtonWrapper as ButtonBase } from '../button/styled-components.ts';

export const ButtonWrapper = styled(ButtonBase)`
  font-weight: bold;
`;
```

```ts
// components/bold-button/index.tsx

import * as React from 'react';
import * as S from './styled-components';


interface IBoldButtonProps {
  children?: any
  onClick?: () => void
}

export const BoldButton = (props: IBoldButtonProps) => {
  return (
    <S.ButtonWrapper {...props}>
      {props.children}
    </S.ButtonWrapper>
  );
};
```