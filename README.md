# d3-axis

坐标轴组件可以将 [scales](https://github.com/d3/d3-scale) 显示为人类友好的刻度标尺参考，减轻了在可视化中的视觉任务。

## Installing

使用 `NPM` 安装: `npm install d3-axis`, 还可以下载 [latest release(最新版)](https://github.com/d3/d3-axis/releases/latest)。此外还可以直接从 [d3js.org](https://d3js.org) 以 [standalone library(标准库)](https://d3js.org/d3-axis.v1.min.js) 或者作为 [D3 4.0](https://github.com/d3/d3) 的一部分直接载入(实际使用时可能还需要 [d3-scale](https://github.com/d3/d3-scale) 和 [d3-selection](https://github.com/d3/d3-selection) 但是并没有依赖关系)。支持 `AMD`，`CommonJS` 以及标签引入形式，如果使用标签引入则会暴露全局 `d3` 变量:

```html
<script src="https://d3js.org/d3-axis.v1.min.js"></script>
<script>

var axis = d3.axisLeft(scale);

</script>
```

[在浏览器中测试 d3-axis](https://tonicdev.com/npm/d3-axis)

## API Reference

无论坐标轴的方向如何，都以原点为起点开始渲染。如果要改变坐标轴的位置，则需要通过 [变换属性](http://www.w3.org/TR/SVG/coords.html#TransformAttribute)来实现，例如：

```js
d3.select("body").append("svg")
    .attr("width", 1440)
    .attr("height", 30)
  .append("g")
    .attr("transform", "translate(0,30)")
    .call(axis);
```

坐标轴组件创建的元素遵循元素公共 API，因此可以自由的设置外部样式或者修改元素来 [customize the axis appearance(自定义器表现形式)](https://bl.ocks.org/mbostock/3371592)

[<img alt="Custom Axis" src="https://raw.githubusercontent.com/d3/d3-axis/master/img/custom.png" width="420" height="219">](http://bl.ocks.org/mbostock/3371592)

坐标轴组件包含类名为 “domain” 的 [path元素](https://www.w3.org/TR/SVG/paths.html#PathElement) 表示比例尺的输入范围，一组类名为 “tick” 的并且被坐标变换的 [g elements](https://www.w3.org/TR/SVG/struct.html#Groups) 表示比例尺的刻度。每个刻度包含一个 [line element](https://www.w3.org/TR/SVG/shapes.html#LineElement) 表示刻度线以及一个 [text element](https://www.w3.org/TR/SVG/text.html#TextElement) 表示刻度标签。例如，刻度朝下的坐标轴组件结构如下：

```html
<g fill="none" font-size="10" font-family="sans-serif" text-anchor="middle">
  <path class="domain" stroke="#000" d="M0.5,6V0.5H880.5V6"></path>
  <g class="tick" opacity="1" transform="translate(0.5,0)">
    <line stroke="#000" y2="6"></line>
    <text fill="#000" y="9" dy="0.71em">0.0</text>
  </g>
  <g class="tick" opacity="1" transform="translate(176.5,0)">
    <line stroke="#000" y2="6"></line>
    <text fill="#000" y="9" dy="0.71em">0.2</text>
  </g>
  <g class="tick" opacity="1" transform="translate(352.5,0)">
    <line stroke="#000" y2="6"></line>
    <text fill="#000" y="9" dy="0.71em">0.4</text>
  </g>
  <g class="tick" opacity="1" transform="translate(528.5,0)">
    <line stroke="#000" y2="6"></line>
    <text fill="#000" y="9" dy="0.71em">0.6</text>
  </g>
  <g class="tick" opacity="1" transform="translate(704.5,0)">
    <line stroke="#000" y2="6"></line>
    <text fill="#000" y="9" dy="0.71em">0.8</text>
  </g>
  <g class="tick" opacity="1" transform="translate(880.5,0)">
    <line stroke="#000" y2="6"></line>
    <text fill="#000" y="9" dy="0.71em">1.0</text>
  </g>
</g>
```

坐标轴的方向是固定的，如果要改变方向，则要移除旧的并重新创建一个新的坐标轴。

<a name="axisTop" href="#axisTop">#</a> d3.<b>axisTop</b>(<i>scale</i>) [<源码>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L159 "Source")

使用给定的 [scale](https://github.com/d3/d3-scale) 构建一个刻度在上的坐标轴生成器, 默认 [tick arguments](#axis_ticks) 为空, [tick size](#axis_tickSize) 为 6， [padding](#axis_tickPadding) 为 3. 坐标轴为水平方向

<a name="axisRight" href="#axisRight">#</a> d3.<b>axisRight</b>(<i>scale</i>) [<源码>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L163 "Source")

使用给定的 [scale](https://github.com/d3/d3-scale) 构建一个刻度在右的坐标轴生成器, 默认 [tick arguments](#axis_ticks) 为空, [tick size](#axis_tickSize) 为 6， [padding](#axis_tickPadding) 为 3. 坐标轴为垂直方向

<a name="axisBottom" href="#axisBottom">#</a> d3.<b>axisBottom</b>(<i>scale</i>) [<源码>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L167 "Source")

使用给定的 [scale](https://github.com/d3/d3-scale) 构建一个刻度在下的坐标轴生成器, 默认 [tick arguments](#axis_ticks) 为空, [tick size](#axis_tickSize) 为 6， [padding](#axis_tickPadding) 为 3. 坐标轴为水平方向

<a name="axisLeft" href="#axisLeft">#</a> d3.<b>axisLeft</b>(<i>scale</i>) [<源码>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L171 "Source")

使用给定的 [scale](https://github.com/d3/d3-scale) 构建一个刻度在左的坐标轴生成器, 默认 [tick arguments](#axis_ticks) 为空, [tick size](#axis_tickSize) 为 6， [padding](#axis_tickPadding) 为 3. 坐标轴为垂直方向

<a name="_axis" href="#_axis">#</a> <i>axis</i>(<i>context</i>) [<源码>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L40 "Source")

将坐标轴渲染到指定的 *context*， *context* 可能是一个包含SVG元素的 [selection](https://github.com/d3/d3-selection)(SVG 或者 G 元素) 也可能是一个 [transition](https://github.com/d3/d3-transition).

<a name="axis_scale" href="#axis_scale">#</a> <i>axis</i>.<b>scale</b>([<i>scale</i>]) [<源码>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L120 "Source")

如果指定了 *scale* 则设置坐标轴的 [scale](https://github.com/d3/d3-scale)，如果没有指定 *scale* 则返回当前坐标轴所使用的比例尺。

<a name="axis_ticks" href="#axis_ticks">#</a> <i>axis</i>.<b>ticks</b>(<i>arguments…</i>) [<源码>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L124 "Source")
<br><a href="#axis_ticks">#</a> <i>axis</i>.<b>ticks</b>([<i>count</i>[, <i>specifier</i>]])
<br><a href="#axis_ticks">#</a> <i>axis</i>.<b>ticks</b>([<i>interval</i>[, <i>specifier</i>]])

在 [坐标轴](#_axis) 渲染时将传入的 *arguments* 传递给 [*scale*.ticks](https://github.com/d3/d3-scale/blob/master/README.md#continuous_ticks) 和 [*scale*.tickFormat](https://github.com/d3/d3-scale/blob/master/README.md#continuous_tickFormat) 并且返回当前坐标轴生成器. 也就是 *arguments* 依赖 [axis’ scale](#axis_scale): 大多数情况下建议传入一个期望的 `ticks` 个数: *count* (或者当使用时间比例尺时传入 [time *interval*](https://github.com/d3/d3-time)), 或者是 [format *specifier*](https://github.com/d3/d3-format) 定义刻度的展示格式。

这个方法有局限，当使用 [band](https://github.com/d3/d3-scale/blob/master/README.md#band-scales) 和 [point](https://github.com/d3/d3-scale/blob/master/README.md#point-scales) 比例尺时没有作用，但是 [*axis*.tickValues](#axis_tickValues). 和 [*axis*.tickFormat](#axis_tickFormat) 不受比例尺类型限制。

比如当使用国际单位格式并且刻度参考个数为 `20` 的线性比例尺:

```js
axis.ticks(20, "s");
```

每隔 15 分钟生成一个刻度的时间比例尺：

```js
axis.ticks(d3.timeMinute.every(15));
```

这个方法也可以看做是 [*axis*.tickArguments](#axis_tickArguments) 的简写，例如：

```js
axis.ticks(10);
```

等价于:

```js
axis.tickArguments([10]);
```

<a name="axis_tickArguments" href="#axis_tickArguments">#</a> <i>axis</i>.<b>tickArguments</b>([<i>arguments</i>]) [源>源码](https://github.com/d3/d3-axis/blob/master/src/axis.js#L128 "Source")

如果设置了 *arguments* 则将其传递给 [*scale*.ticks](https://github.com/d3/d3-scale/blob/master/README.md#continuous_ticks) 和 [*scale*.tickFormat](https://github.com/d3/d3-scale/blob/master/README.md#continuous_tickFormat) 并且返回当前坐标轴生成器。也就是 *arguments* 依赖 [axis’ scale](#axis_scale): 大多数情况下建议传入一个期望的 `ticks`个数: *count* (或者当使用时间比例尺时传入 [time *interval*](https://github.com/d3/d3-time)), 或者是 [format *specifier*](https://github.com/d3/d3-format) 定义刻度的展示格式。

这个方法有局限，当使用 [band](https://github.com/d3/d3-scale/blob/master/README.md#band-scales) 和 [point](https://github.com/d3/d3-scale/blob/master/README.md#point-scales) 比例尺时没有作用，但是 [*axis*.tickValues](#axis_tickValues). 和 [*axis*.tickFormat](#axis_tickFormat) 不受比例尺类型限制。

如果没有指定 *arguments* 则返回当前的 `tick` 参数，默认是一个空数组。

比如当使用国际单位格式并且刻度参考个数为 20 的线性比例尺:

```js
axis.tickArguments([20, "s"]);
```

每隔 15 分钟生成一个刻度的时间比例尺：

```js
axis.tickArguments([d3.timeMinute.every(15)]);
```

参考 [*axis*.ticks](#axis_ticks).

<a name="axis_tickValues" href="#axis_tickValues">#</a> <i>axis</i>.<b>tickValues</b>([<i>values</i>]) [<源码>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L132 "Source")

如果指定了 *values* 数组，则使用指定的数组作为刻度而不是自动计算刻度。如果 *values* 为 `null` 则清除之前设置的显示刻度参数，也就是如果之前设置过*values* 则可以使用 `null` 将其取消。如果没有指定 *values* 则返回当前的刻度值参数，默认为 `null`。例如使用指定的数组作为刻度：

```js
var xAxis = d3.axisBottom(x)
    .tickValues([1, 2, 3, 5, 8, 13, 21]);
```

通过 *axis.tickValues* 设置刻度的优先级大于通过 [*axis*.tickArguments](#axis_tickArguments) 设置的优先级。但是如果没有设置格式化仍然会参考[tickFormat](#axis_tickFormat) 去对文本标签进行格式化。

<a name="axis_tickFormat" href="#axis_tickFormat">#</a> <i>axis</i>.<b>tickFormat</b>([<i>format</i>]) [<源码>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L136 "Source")

如果指定了 *format* 则设置刻度文字标签格式化方法。如果没有指定 *format* 则返回当前的刻度文本格式化方法，默认为 `null`。在没有设置格式化方法的情况下，会使用默认的 [*scale*.tickFormat](https://github.com/d3/d3-scale/blob/master/README.md#continuous_tickFormat) 去生成刻度文本. 在这种情况下通过 [*axis*.tickArguments](#axis_tickArguments) 设置的格式化方法会直接被 *scale*.tickFormat 使用

参考 [d3-format](https://github.com/d3/d3-format) 和 [d3-time-format](https://github.com/d3/d3-format) 获取关于格式化的更多信息。例如，要使用逗号分组来表示千分位数：

```js
axis.tickFormat(d3.format(",.0f"));
```

为方便，可以直接将格式化字符串通过以下形式直接传递给 [*axis*.ticks](#axis_ticks):

```js
axis.ticks(10, ",f");
```

使用这种方法可以基于刻度间隔自动设置精度.

<a name="axis_tickSize" href="#axis_tickSize">#</a> <i>axis</i>.<b>tickSize</b>([<i>size</i>]) [<源码>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L140 "Source")

如果指定了 *size* 则设置 [内侧](#axis_tickSizeInner) 和 [外侧](#axis_tickSizeOuter) 刻度的大小，并返回坐标轴生成器。如果没有指定 *size* 则返回当前的刻度大小，默认为 6。

<a name="axis_tickSizeInner" href="#axis_tickSizeInner">#</a> <i>axis</i>.<b>tickSizeInner</b>([<i>size</i>]) [源>源码](https://github.com/d3/d3-axis/blob/master/src/axis.js#L144 "Source")

如果指定了 *size* 则设置内侧刻度大小，如果没有指定 *size* 则返回当前的刻度大小，默认为 6。内侧刻度大小控制着刻度线的长度。

<a name="axis_tickSizeOuter" href="#axis_tickSizeOuter">#</a> <i>axis</i>.<b>tickSizeOuter</b>([<i>size</i>]) [源>源码](https://github.com/d3/d3-axis/blob/master/src/axis.js#L148 "Source")

如果指定了 *size* 则设置外侧刻度大小，如果没有指定 *size* 则返回当前的刻度大小，默认为 6。外侧刻度大小控制着刻度线的长度。外侧刻度表示的是坐标轴最外侧两端的刻度线。内侧刻度和外侧刻度不同，内侧刻度是一个个单独的 `line` 元素，而外侧刻度则实际上是坐标轴线 `path` 的一部分。此外外侧刻度可能和第一个或最后一个内侧刻度重合。

<a name="axis_tickPadding" href="#axis_tickPadding">#</a> <i>axis</i>.<b>tickPadding</b>([<i>padding</i>]) [源>源码](https://github.com/d3/d3-axis/blob/master/src/axis.js#L152 "Source")

如果设置了 *padding* 则设置刻度和刻度文本之间的间距，如果没有指定 *padding* 则返回当前的间距，默认为 3 像素。
