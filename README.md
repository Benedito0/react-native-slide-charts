# react-native-slide-charts

[![Version](https://img.shields.io/npm/v/react-native-slide-charts.svg)](https://www.npmjs.com/package/react-native-slide-charts)
[![NPM](https://img.shields.io/npm/dm/react-native-slide-charts.svg)](https://www.npmjs.com/package/react-native-slide-charts)

`react-native-slide-charts` uses [`react-native-svg`](https://github.com/react-native-community/react-native-svg), [`d3`](https://github.com/d3/d3), and [`react-native-gesture-handler`](https://github.com/software-mansion/react-native-gesture-handler) to create highly customizable interactive charts that animate smoothly via [`Direct Manipulation`](https://facebook.github.io/react-native/docs/direct-manipulation).

## [Check out the demo on expo](https://snack.expo.io/@nhannah/react-native-slide-charts)

## Features

### Bar Chart

![](./screenshots/BarChart.gif)

### Area Chart

![](./screenshots/AreaChart.gif)

## Installation

```console
$ npm install react-native-slide-charts --save
```

or

```console
$ yarn add react-native-slide-charts
```

### Peer Dependencies

`react-native-slide-charts` depends on three peer dependencies with native modules that must be installed alongside it. Follow the installation instructions for both iOS and Android for all three packages.

| Package                                                                                               | Minimum Version | Maximum Version |
| ----------------------------------------------------------------------------------------------------- | --------------- | --------------- |
| [`react-native-svg`](https://github.com/react-native-community/react-native-svg)                      | 7.0.0           | 9.x             |
| [`react-native-gesture-handler`](https://github.com/software-mansion/react-native-gesture-handler)    | 1.1.0           | 1.x             |
| [`react-native-haptic-feedback`](https://github.com/milk-and-cookies-io/react-native-haptic-feedback) | 1.8.0           | 1.x             |

#### NOTICE:

Make sure the version of the native module packages chosen works with the `react-native` version of the project. Manually linking the projects may be required depending on the version and platform.

## Usage

`react-native-slide-charts` exports two types of charts, `SlideAreaChart` and `SlideBarChart` along with the type definitions for the charts, Props, and enums.

```jsx
import {
  SlideAreaChart,
  SlideBarChart,
  SlideBarChartProps,
  SlideAreaChartProps,
  YAxisProps,
  XAxisProps,
  XAxisMarkerProps,
  XAxisLabelAlignment,
  YAxisLabelAlignment,
  LabelAndAlignment,
  CursorProps,
  ToolTipProps,
  ToolTipTextRenderersInput,
  GradientProps,
} from 'react-native-slide-charts'
```

### Charts

#### Common Props:

<table>
<thead>
<tr>
<td align="center">
  Prop
</td>
<td align="center">
  Type
</td>
<td align="center">
  Default
</td>
<td align="left">
  Note
</td>
</tr>
</thead>
<tbody>
<tr>
<td align="center">
  
  ##### `alwaysShowIndicator`
</td>
<td align="center">

`boolean`

</td>
<td align="center">

`true`

</td>
<td align="left">

Determines if the indicator for the chart should be visible always or just when being touched.<br/><br/>For `SlideAreaChart` the indicator is the `CursorMarker`, `CursorLine`, and `ToolTip`.<br/><br/>For `SlideBarChart` the indicator is the `barSelectedColor` or `renderSelectedFillGradient` and `ToolTip`.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `animated`
</td>
<td align="center">

`boolean`

</td>
<td align="center">

`true`

</td>
<td align="left">

Animates the charts on mounting and between prop updates.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `axisHeight`
</td>
<td align="center">

`number`

</td>
<td align="center">

`0`

</td>
<td align="left">

Height of the area below the chart for the X-Axis markers and label to render in.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `axisWidth`
</td>
<td align="center">

`number`

</td>
<td align="center">

`0`

</td>
<td align="left">

Width of the area left of the chart for the Y-Axis markers and label to render in.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `callbackWithX`
</td>
<td align="center">

```ts
(x: number | Date)
=> void
```

</td>
<td align="center">

`undefined`

</td>
<td align="left">

Callback function that provides the current cursor position `x`. As this is firing off of a continuous animation and not state usage should match appropriately.<br/><br/>e.g. This can be used in conjunction with an array of timed gps points to move an indicator along a path on a map.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `callbackWithY`
</td>
<td align="center">

```ts
(y: number)
=> void
```

</td>
<td align="center">

`undefined`

</td>
<td align="left">

Callback function that provides the current cursor position `y`. As this is firing off of a continuous animation and not state usage should match appropriately.<br/><br/>e.g. This can be used with direct manipulation on a `TextInput` to display the current value outside the chart.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `data`
</td>
<td align="center">

```ts
Array<{
  x: number
  | Date,
  y: number
}>
```

</td>
<td align="center">

`[]`

</td>
<td align="left">

Data that will be displayed on the chart. This must be an array of object with `x` and `y` values with the `x` increasing as the chart does not sort the array before use and will render incorrectly otherwise.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `chartPaddingTop`
</td>
<td align="center">

`number`

</td>
<td align="center">

`16`

</td>
<td align="left">

TODO: LINK
Pushes the rendered height of the data within the chart down to make room for the `ToolTip` at the max. The `ToolTip` will render outside of the chart component if desired so this can be set to `0` or adjusted for using [`paddingTop`](#paddingtop) or [`style`](#style) if desired.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `height`
</td>
<td align="center">

`number`

</td>
<td align="center">

`200`

</td>
<td align="left">

Height of the entire chart component.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `onPress`
</td>
<td align="center">

```ts
() => void
```

</td>
<td align="center">

`undefined`

</td>
<td align="left">

If provided the chart will not be interactive and instead can be pressed.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `paddingBottom`
</td>
<td align="center">

`number`

</td>
<td align="center">

`0`

</td>
<td align="left">

Bottom padding as it can not be applied via styles to the chart component.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `paddingLeft`
</td>
<td align="center">

`number`

</td>
<td align="center">

`8`

</td>
<td align="left">

Left padding as it can not be applied via styles to the chart component.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `paddingRight`
</td>
<td align="center">

`number`

</td>
<td align="center">

`8`

</td>
<td align="left">

Right padding as it can not be applied via styles to the chart component.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `paddingTop`
</td>
<td align="center">

`number`

</td>
<td align="center">

`0`

</td>
<td align="left">

Top padding as it can not be applied via styles to the chart component.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `renderFillGradient`
</td>
<td align="center">

```ts
(props:
GradientProps)
=> JSX.Element
| null
```

</td>
<td align="center">

TODO: PUT GRADIENT

</td>
<td align="left">

Function that returns a custom gradient to fill the bars of the bar chart or area of the area chart.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `scrollable`
</td>
<td align="center">

`boolean`

</td>
<td align="center">

`undefined`

</td>
<td align="left">

Ensure touch is passed to `scrollView` on `y` movement if component is inside `scrollView`.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `shouldCancelWhenOutside`
</td>
<td align="center">

`boolean`

</td>
<td align="center">

`true`

</td>
<td align="left">

Terminates touch outside the chart component.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `showIndicatorCallback`
</td>
<td align="center">

```ts
(opacity: number)
=> void
```

</td>
<td align="center">

`undefined`

</td>
<td align="left">

If [`alwaysShowIndicator`](#alwaysshowindicator) is `false` this function is fired with the current indicator opacity whenever the indicator appears or disappears.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `style`
</td>
<td align="center">

`ViewStyle`

</td>
<td align="center">

```ts
{
backgroundColor:
'#fff'
}
```

</td>
<td align="left">

Style of chart component.

</td>
</tr>
</tr>
<tr>
<td align="center">
  
  ##### `throttleAndroid`
</td>
<td align="center">

`boolean`

</td>
<td align="center">

`false`

</td>
<td align="left">

On some slower Android devices there may be too many calls across the bridge that it can cause some lagging of the indicator movement, this limits the calls to the queue on Android with little noticeable change in the interaction.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `toolTipProps`
</td>
<td align="center">

TODO:LINK<br/>
`ToolTipProps`

</td>
<td align="center">

`undefined`

</td>
<td align="left">

Props for rendering the `ToolTip`.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `width`
</td>
<td align="center">

`number`

</td>
<td align="center">

```ts
Dimensions
.get('window')
.width
```

</td>
<td align="left">

Width of the entire chart.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `xAxisProps`
</td>
<td align="center">

TODO: LINK<br/>
`XAxisProps`

</td>
<td align="center">

`undefined`

</td>
<td align="left">

Props for rendering the `XAxis`.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `xRange`
</td>
<td align="center">

```ts
[number, number]
| [Date, Date]
```

</td>
<td align="center">

Value of `x` in first and last object in [`data`](#data) array.

</td>
<td align="left">

TODO: Link
The range for the `XAxis` of the chart to be rendered using.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `xScale`
</td>
<td align="center">

```ts
'time' | 'linear'
```

</td>
<td align="center">

`'linear'`

</td>
<td align="left">

Determines the applied [`d3` scale](https://www.d3indepth.com/scales/) of the chart.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `yAxisProps`
</td>
<td align="center">

TODO: link<br/>
`YAxisProps`

</td>
<td align="center">

`undefined`

</td>
<td align="left">

Props for rendering the YAxis.

</td>
</tr>
<tr>
<td align="center">
  
  ##### `yRange`
</td>
<td align="center">

```ts
[number, number]
```

</td>
<td align="center">

Max and Min value of `y` in [`data`](#data) array

</td>
<td align="left">

TODO: link
The range for the `YAxis` of the chart to be rendered using.

</td>
</tr>
</tbody>
</table>
