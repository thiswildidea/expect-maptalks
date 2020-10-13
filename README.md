# expect-cmap

[![Circle CI](https://circleci.com/gh/cmap/expect-cmap.svg?style=shield)](https://circleci.com/gh/cmap/expect-cmap)

A plugin of expect.js(https://github.com/Automattic/expect.js) for cmap with assertions for Coordinate/GeoJSON/Layer

## Usage

```bash
npm install expect-cmap --save-dev
```

### with Karma
Install [karma-expect-cmap](https://github.com/thiswildidea/karma-expect-cmap)
```bash
npm install karma-expect-cmap --save-dev
```
In karma.conf.js, Attention: **always declare expect-cmap behind expect**
```javascript
    frameworks: [
      'mocha',
      'expect',
      'expect-cmap'
    ],
    
    plugins: [
      'karma-expect',
      'karma-expect-cmap'
    ],
```


## Methods

**approx**: asserts that the value is approximately equal or not

```js
expect(1.000001).to.be.approx(1);
expect(1.001).to.be.approx(1, 1E-2);
```

**closeTo**: asserts that whether the coordinate is closeTo another (approx with a delta of 1E-6)

```js
expect([1, 1]).to.be.closeTo([1 + 1E-7, 1 - 1E-7]);
expect({x : 1, y : 1}).to.be.closeTo([1 + 1E-7, 1 - 1E-7]);
```

**eqlGeoJSON**: asserts that whether a GeoJSON object is equal with another (true if the coordinates are closeTo another's)

```js
//true
expect({ "type": "Point", "coordinates": [0.0, 0.0] })
    .to.be.eqlGeoJSON({ "type": "Point", "coordinates": [0.000001, 0.000001] });
```

**painted**: asserts the given layer or map is painted in the center with a offset.

```js
var v = new cmap.VectorLayer('v').addGeometries(geos).addTo(map);
//asserts layer is painted in the center
expect(v).to.be.painted();
//whether the layer is painted with an offset {x:5, y:3} from the center.
//a negative x to the left and a positive to the right.
//a negative y to the top and a positive to the bottom.
expect(v).to.be.painted(5, 3);
//assert the point's color is [255, 255, 255]
expect(v).to.be.painted(5, 3, [255, 255, 255]);
//also support map
expect(map).to.be.painted(5, 3, [255, 255, 255]);
```
