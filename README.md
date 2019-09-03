# React SVG Brush (Beta)

A React-based brush library that emulates the [d3-brush](https://github.com/d3/d3-brush) behavior. It renders the brush using React virtual DOM.

This library is still in Beta, please file bug report directly to the author.

## Why Yet Another Brush Library

The [d3-brush](https://github.com/d3/d3-brush) library is commonly used for data selection within visualizations. It enables data selection through dragging on the visualization interface (holding the left mouse and move the curser). It also renders the brushed area directly on the visualization. However, there are several drawbacks when using [d3-brush](https://github.com/d3/d3-brush) directly inside a React-based application:

- d3-brush directly modifies the DOM, which also means customization of the brush behavior/view has to be done directly on the DOM, violating the best practices in React.
- Using d3-brush inside a React component typically requires using the react lifecycle methods, e.g. `componentDidUpdate`, adding complexity in the implementation of the React component.

The React SVG Brush library emulates the d3-brush library DOM structure (95% identical) and functionalities but renders the Brush completely using the React virtual DOM, making it easy for applications that use d3-brush to switch to this library to adhere to the React best practices.

## Installation

```
npm install react-svg-brush
```

## Example Usage

```javascript
import React, {Component} from 'react';
import SVGBrush from 'react-svg-brush';

...

export default class App extends Component {
  onBrushStart = ({target, type, selection, sourceEvent})=>{...}
  onBrush = ({target, type, selection, sourceEvent})=>{...}
  onBrushEnd = ({target, type, selection, sourceEvent})=>{...}
  renderBrush = () => (
    <SVGBrush
      // Defines the boundary of the brush.
      // Strictly uses the format [[x0, y0], [x1, y1]] for both 1d and 2d brush.
      // Note: d3 allows the format [x, y] for 1d brush.
      extent={[[x0, y0], [x1, y1]]}
      // Obtain mouse positions relative the current svg during mouse events.
      // By default, getEventMouse returns [event.clientX, event.clientY]
      getEventMouse={event => {
        const {clientX, clientY} = event;
        const {left, top} = this.svg.getBoundingClientRect();
        return [clientX - left, clientY - top];
      }}
      brushType="2d" // "x"
      onBrushStart={this.onBrushStart}
      onBrush={this.onBrush}
      onBrushEnd={this.onBrushEnd}
    />
  )
  render() {
    return (
      <svg ref={input => (this.svg = input)}>
        {this.renderBrush()}
      </svg>
    );
  }
}
```

The following shows the DOM structure generated by React SVG Brush:

![](/docs/dom-structure.png)

More demo code can be found in this repo, [React SVG Brush Example](https://github.com/kenns29/react-svg-brush-example).

## API Reference

... work in progress ...
