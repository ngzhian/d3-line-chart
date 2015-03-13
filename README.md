d3-line-chart
=============

[![d3-line-chart API Documentation](https://www.omniref.com/js/npm/d3-line-chart.png)](https://www.omniref.com/js/npm/d3-line-chart)

A d3.js library to help you draw line charts easily.

## How to use it
- include `d3.js`, `d3-line-char.js`
```javascript
<script type="text/javascript" src="./d3.js" charset="utf-8"></script>
<script type="text/javascript" src="./d3-line-chart.js" charset="utf-8"></script>
```
- simplest way to draw the graph
```javascript
	var data = {
		name: 'series',
		values: [{x: 1, y: 2}, {x: 2, y : 4}, {x:3, y: 3}]
	};
	new LineChart().for([data]).plot();
```

![d3-line-chart](https://raw.githubusercontent.com/ngzhian/d3-line-chart/master/d3-line-chart.png "a simple line chart drawn with d3-line-chart")

This library uses [UMD](https://github.com/umdjs/umd/blob/master/returnExports.js) to export a single name to the browser window: "`LineChart`". It has a single dependency on `d3` and expects it to be exported to the browser window as well, include `d3` using the `<script>` tag and you will be fine.

If you ever use this on nodejs, you can use `require` as such
```javascript
var LineChart = require('./d3-line-chart.js');
```

## API
d3-line-chart actually provides a lot more options for drawing line chart, you can customize the following things.
- `id` of the svg chart, defaults to no id
- `parent` of the chart, defaults to `body`
- `all_series` an array of series that will be plotted
- `graph-width`, width of the entire graph, defaults to 960
- `graph-height`, height of the entire graph, defaults to 500
-	`margin`, margins around the chart, this can be used to draw axis and legent, defaults to (20, 100, 30, 60)
- `x_axis_text` text that is printed beside the x-axis
- `y_axis_text` text that is printed beside the y-axis
- `x_parse` function that is used to parse the `x` values of each data point, defaults to identity function
- `y_parse` function that is used to parse the `y` values of each data point, defaults to identity function
-	`x_scale` scale function for `x` values, defaults to `d3.scale.linear()` 
-	`y_scale` scale function for `y` values, defaults to `d3.scale.linear()`
- `width` the maximum width the line chart can appear in, equals to `graph_width - margin.left - margin.right`, defaults to 960 - 100 - 60
- `height` the maximum height the line chart can appear in, equals to `graph_height - margin.right - margin.bottom`, defaults to 500 - 20 - 30
- `tooltip` a function that is called with the tooltip div and the current data point that is hovered to allow you to display your custom div

## More advanced stuff

### Specify colours
The color for reach series is taken from `d3.scale.category10()`, which is used to provide a mapping from the `name` of a series to one of ten available colours. If more colours are needed, you need to edit the source, to use `d3.scale.category20()` perhaps.

### Tooltips on hover
By default tooltips are shown on hover, with some simple styling. `x-axis` values are underlined, followed by `y-axis` values.

You can display your own custom tooltip by providing a function called `tooltip` to the constructor. This function must take in 2 parameters, `div`, which is the div of the tooltip, and `point` which is the point that is hovered over.

### Date on the x axis
You can specify other scales besides `d3.scale.linear()` by passing the function into `LineChart()`
``` javascript
lc = new LineChart({
	x_scale: d3.time.scale()
});
var data = {
	name: 'series',
	values: [{x: new Date(2014, 4, 1, 0, 0, 0, 0), y: 9},
	{x: new Date(2014, 4, 3, 0, 0, 0, 0), y: 2},
	{x: new Date(2014, 4, 9, 0, 0, 0, 0), y: 3}]
};
lc.for([data]).plot();
```
