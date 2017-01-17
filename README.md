# tipsi-ui-kit
React Native Tipsi custom UI elements

## Components

### `<ColoredTabs />`

Customizable colored tabs.

#### ColoredTabs Props

| Name | Desc | Type | Default
| --- | --- | --- | --- |
| `selected` | id of selected tab.  | String | `undefined`
| `onPress` | Handle press on tab action. Receive id of selected tab as argument. | Function | `undefined`


#### ColoredTabs.Item Props

| Name | Desc | Type | Default
| --- | --- | --- | --- |
| `name` | Text of tab. | String | `undefined`
| `color` | Color of tab | String | `undefined`
| `id` | Tab id. This id will passed to `onPress` for identify action. | String | `undefined`
| `active` | Show item as active  | Boolean | `false`
| `onPress` | Handle press action | Function | `undefined`

#### Example

```js
import React from 'react'
import { ColoredTabs } from 'tipsi-ui-kit'

handlePress = (id) => (console.log(`Tab with id ${id} is clicked!`)

const Example = () => (
    <ColoredTabs onPress={this.handlePress}>
      <ColoredTabs.Item id="0" name="One" color="crimson" />
      <ColoredTabs.Item id="1" name="Two" color="orange" />
      <ColoredTabs.Item id="2" name="Three" color="chartreuse" />
      <ColoredTabs.Item id="3" name="Four" color="dodgerblue" />
    < /ColoredTabs>
)
```

#### Preview

![tabs_ios](https://cloud.githubusercontent.com/assets/4946753/22029399/1f3905c2-dce3-11e6-8c83-5142fdeb4351.png)
![tabs_android](https://cloud.githubusercontent.com/assets/4946753/22029396/1af713e6-dce3-11e6-8f1a-64e4706bf581.png)

### `<Dash />`

Component to draw customisable dashed lines

#### Dash Props

| Name | Desc | Type | Default
| --- | --- | --- | --- |
| `style` | Dash container style as for `View` component  | Object | `{flexDirection = 'row'}`
| `dashGap` | Gap between two dashes | Number | `3.5`
| `dashLength` | Length of each dash | Number | `3`
| `dashThickness` | Thickness of each dash | Number | `1`
| `dashColor` | Color of each dash | String | `#c7d1dc`

#### Example

```js
import React from 'react'
import { Dash } from 'tipsi-ui-kit'

const Example = () => (
  <Dash
    dashGap={5}
    dashLength={10}
    dashThickness={2}
    dashColor="black"
  />
)
```

#### Preview

![dash_ios](https://cloud.githubusercontent.com/assets/1177226/21903147/5d0b07d4-d931-11e6-9ff4-3238f0646d0b.png)
![dash_android](https://cloud.githubusercontent.com/assets/1177226/21903095/2181a7cc-d931-11e6-9338-17e32c8817ea.png)

### `<Carousel />`

Carousel component

#### Carousel Props

| Name | Desc | Type | Default
| --- | --- | --- | --- |
| `spacer` | Space between last item and right side  | Number | `0`
| `...rest` | All other props for `ScrollView` component except `horizontal` | - | `-`


#### Carousel.Item Props

| Name | Desc | Type | Default
| --- | --- | --- | --- |
| `active` | Show item as active  | Boolean | `false`
| `onPress` | Handle press action | Function | `undefined`
| `onRemove` | Handle remove action | Function | `undefined`
| `activeStyle` | Styles for active item | Object | `undefined`

#### Example

```js
import React from 'react'
import { Text } from 'react-native'
import { Carousel } from 'tipsi-ui-kit'

const Example = () => (
  <Carousel spacer={10}>
    <Carousel.Item active>
      <Text>Facebook</Text>
    </Carousel.Item>
    <Carousel.Item>
      <Text>Twitter</Text>
    </Carousel.Item>
    <Carousel.Item active>
      <Text>Instagram</Text>
    </Carousel.Item>
    <Carousel.Item>
      <Text>YouTube</Text>
    </Carousel.Item>
    <Carousel.Item active>
      <Text>Tumblr</Text>
    </Carousel.Item>
  </Carousel>
)
```

#### Preview

![carousel_ios](https://cloud.githubusercontent.com/assets/1177226/21901928/7a710d78-d92c-11e6-965c-762c2e598811.gif)
![carousel_android](https://cloud.githubusercontent.com/assets/1177226/21901929/7c64d948-d92c-11e6-8ce5-793f24ec2300.gif)

## UIExplorer

To open `UIExplorer` just start mobile app with the `react-native` command:

```bash
react-native run-ios
# OR
react-native run-android
```

## How to add new UI component

For example let's create `Button` component:

1. Create a new directory called `Button` in `src` directory and create an entry file (index.js) and component file (Button.js) as given below.

  ```js
  // src/Button/Button.js
  import React, { Component, PropTypes } from 'react'
  import { Button as RNButton } from 'react-native'

  export default class Button extends Component {
    static propTypes = {
      title: PropTypes.string.isRequired,
      onPress: PropTypes.func,
    }

    render() {
      return (
        <RNButton
          title={this.props.title}
          onPress={this.props.onPress}
        />
      )
    }
  }

  // src/Button/index.js
  export { default } from './Button'
  ```

2. Update `src` entry file (index.js) to export our new component:

  ```js
  // src/index.js
  export { default as StarRating } from './StarRating'
  // ...
  export { default as Button } from './Button' // Add this line
  ```

3. Then write your example in `uiexplorer/examples` directory like this:
  ```js
  // uiexplorer/examples/Button.js
  import React, { Component } from 'react'
  import register from '../core/utils/register'
  import Button from '../../src/Button'

  register.addExample({
    type: 'components',
    title: '<Button />',
    description: 'Button component',
    examples: [{
      title: 'Title',
      description: 'Prop: title (String)',
      render: () => (
        <Button title="Example" />
      ),
    }, {
      title: 'Handle press',
      description: 'Prop: onPress (Function)',
      render: ({ action }) => (
        <Button title="Press me!" onPress={action('onPress')} />
      ),
    }],
  })
  ```

4. Update `uiexplorer/examples` entry file (index.js) to export example for our new component:

    ```js
    // uiexplorer/examples/index.js
    import './StarRating'
    // ...
    import './Button' // Add this line
    ```

5. Now you can open `UIExplorer` and click on `<Button />` item to see a result.
