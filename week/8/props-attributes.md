# props & attribute

스타일을 동적으로 조작하는 데 사용되는 기능

## props

[Adapting based on props](https://styled-components.com/docs/basics#adapting-based-on-props)

컴포넌트에 전달된 속성을 스타일에 활용하는 데 사용. props를 활용하여 컴포넌트의 상태나 사용자 입력에 따라 스타일을 동적으로 변경

```javascript
const StyledButton = styled.button`
  font-size: ${(props) => (props.small ? '12px' : '16px')};
`;

// 사용 예시
<StyledButton small>Small Button</StyledButton>
<StyledButton>Regular Button</StyledButton>
```

## attrs

속성을 styled component에 전달하는 역할. tag 속성 / css 속성을 동적으로 변경할 때 사용

```javascript
const StyledButton = styled.button`
  &::before {
    content: attr(data-prefix); // attr을 사용하여 data-prefix 속성 값을 가져옴
  }
`;

// 사용 예시
<StyledButton data-prefix="*" />
```
