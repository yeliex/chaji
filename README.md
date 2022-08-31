# chaji
framework-agnostic css-in-js with react-native, ssr, mini-program support

```tsx
import { StyleSheet, Keyframes, Theme } from '@chaji/core';

const resetButton = StyleSheet.create({
  backgroundColor: 'transparent'
});

// merge in style but generate Animate variables in react native
const transition = Keyframes.create({
  '0%': {},
});

const theme = Theme.create({});

// get style sheet instance
const stylesheet = StyleSheet.create((theme) => [
  resetButton, 
  {
    color: 'red',
    fontSize: 12,
    background: 'none',
    // modify to primary style
    '&--primary': {
      color: 'white',
      background: 'blue'
    },
    '&--large': {
      fontSize: 14
    },
    // children of element
    '&__icon': {
      
    },
    // same as &__icon, but different in generated classname
    '& icon': {
    
    },
    // with hover state
    '&:hover': [transition, {
      
    }]
  }
], {
  prefix: 'button',
  transformClassName: () => {},
});

stylesheet.className // => 'button';
stylesheet.icon.className // => 'button__icon';
stylesheet('primary').className // => 'button__primary';
stylesheet(['primary', 'large']).className // => 'button__primary button__large';

stylesheet.style // => { color: 'red', ... }
stylesheet(['primary', 'large']).style // => { color:'white', fontSize: 14, ... }

stylesheet.icon // => get stylesheet for icon element

// todo: maybe className function has better performance?
stylesheet.className(['primary', 'large'])

// todo: has better solution?
stylesheet.theme = theme
stylesheet.clone().theme = theme

// stylesheet is static after define, modify theme would regenerate

// update dynamicly
stylesheet.update({
// update
});

// generate style instance, cached by theme
const useStyle = (stylesheet, theme) => {
  
}
```
