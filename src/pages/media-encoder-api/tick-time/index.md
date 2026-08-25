---
title: "TickTime: Media Encoder API"
description: "Media Encoder's TickTime API for representing and manipulating time values used by RenderOptions and other scripting objects."
id: tickTime
title: TickTime
sidebar_label: TickTime
product: mediaencoder
keywords:
  - UXP
  - Adobe Media Encoder
  - Media Encoder API
  - TickTime
  - timecode
  - scripting automation


contributors:
  - https://github.com/justintaylor-dev
  - https://github.com/sukriyeLudwig
---

# TickTime

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. This reference is being written, and the supported API surface may change before general availability.

Since: **26.5**

A `TickTime` represents a precise point in time (or duration), used throughout the Media Encoder scripting API wherever a time value is required, such as [RenderOptions.setCustomInAndOutPoints](../render-options/index.md#setcustominandoutpoints).

The `TickTime` class can be accessed from the main app object. Most `TickTime` values are created using one of the `create*` class methods below, rather than the constructor directly:

```javascript
const app = require("mediaencoder");
const startTime = app.TickTime.createWithSeconds(0);
```

<HorizontalLine />

## Constants

These `TickTime` Constants are class properties, accessed via the `TickTime` object itself.

```javascript
const app = require("mediaencoder");
const TIME_ZERO = app.TickTime.TIME_ZERO;
```

### TIME_ZERO

A `TickTime` representing zero.

Type: _object_ (readonly)

Since: **26.5**

<HorizontalLine />

### TIME_ONE_SECOND

A `TickTime` representing one second.

Type: _object_ (readonly)

Since: **26.5**

<HorizontalLine />

### TIME_ONE_MINUTE

A `TickTime` representing one minute.

Type: _object_ (readonly)

Since: **26.5**

<HorizontalLine />

### TIME_ONE_HOUR

A `TickTime` representing one hour.

Type: _object_ (readonly)

Since: **26.5**

<HorizontalLine />

### TIME_MAX

The maximum representable `TickTime`.

Type: _object_ (readonly)

Since: **26.5**

<HorizontalLine />

### TIME_MIN

The minimum representable `TickTime`.

Type: _object_ (readonly)

Since: **26.5**

<HorizontalLine />

### TIME_INVALID

An invalid/sentinel `TickTime` value.

Type: _object_ (readonly)

Since: **26.5**

<HorizontalLine />

## Properties

These read-only instance properties are available on any `TickTime` instance.

```javascript
const app = require("mediaencoder");
const time = app.TickTime.createWithSeconds(1.5);
time.seconds; // 1.5
```

### seconds

The time value in seconds.

Type: _number_ (readonly)

Since: **26.5**

<HorizontalLine />

### ticks

The time value as a ticks string.

Type: _string_ (readonly)

Since: **26.5**

<HorizontalLine />

### ticksNumber

The time value as a ticks number.

Type: _number_ (readonly)

Since: **26.5**

<HorizontalLine />

## Methods

### createWithFrameAndFrameRate

**Class method.** Creates a `TickTime` from a frame count at a given frame rate.

Since: **26.5**

#### Parameters

| Name       | Type     | Description                        |
| :--------- | :------- | :---------------------------------- |
| frameCount | _number_ | The number of frames                |
| frameRate  | _object_ | A FrameRate object                  |

#### Returns

| Name     | Type     | Description                |
| :------- | :------- | :-------------------------- |
| tickTime | _object_ | The resulting `TickTime`   |

```javascript
const app = require("mediaencoder");
const time = app.TickTime.createWithFrameAndFrameRate(30, frameRate);
```

<HorizontalLine />

### createWithSeconds

**Class method.** Creates a `TickTime` from a number of seconds.

Since: **26.5**

#### Parameters

| Name    | Type     | Description             |
| :------ | :------- | :------------------------ |
| seconds | _number_ | The time value in seconds |

#### Returns

| Name     | Type     | Description              |
| :------- | :------- | :------------------------ |
| tickTime | _object_ | The resulting `TickTime` |

```javascript
const app = require("mediaencoder");
const startTime = app.TickTime.createWithSeconds(0);
const endTime = app.TickTime.createWithSeconds(1);
```

<HorizontalLine />

### createWithTicks

**Class method.** Creates a `TickTime` from a ticks string.

Since: **26.5**

#### Parameters

| Name  | Type     | Description        |
| :---- | :------- | :------------------ |
| ticks | _string_ | The ticks string    |

#### Returns

| Name     | Type     | Description              |
| :------- | :------- | :------------------------ |
| tickTime | _object_ | The resulting `TickTime` |

```javascript
const app = require("mediaencoder");
const time = app.TickTime.createWithTicks("254016000000");
```

<HorizontalLine />

### createWithTicksNumber

**Class method.** Creates a `TickTime` from a ticks number.

Since: **26.5**

#### Parameters

| Name        | Type     | Description         |
| :---------- | :------- | :-------------------- |
| ticksNumber | _number_ | The ticks number      |

#### Returns

| Name     | Type     | Description              |
| :------- | :------- | :------------------------ |
| tickTime | _object_ | The resulting `TickTime` |

```javascript
const app = require("mediaencoder");
const time = app.TickTime.createWithTicksNumber(254016000000);
```

<HorizontalLine />

### timecodeToTime

**Class method.** Converts a timecode display string to a `TickTime`.

Since: **26.5**

#### Parameters

| Name            | Type     | Description             |
| :--------------- | :------- | :------------------------ |
| timecodeString   | _string_ | The timecode string to convert |
| frameRate        | _object_ | A FrameRate object      |
| timeDisplay      | _object_ | A TimeDisplay object    |

#### Returns

| Name     | Type     | Description              |
| :------- | :------- | :------------------------ |
| tickTime | _object_ | The resulting `TickTime` |

```javascript
const app = require("mediaencoder");
const time = app.TickTime.timecodeToTime("00:00:01:00", frameRate, timeDisplay);
```

<HorizontalLine />

### timeToTimecode

**Class method.** Converts a `TickTime` to a timecode display string.

Since: **26.5**

#### Parameters

| Name        | Type     | Description           |
| :----------- | :------- | :----------------------- |
| tickTime    | _object_ | The `TickTime` to convert |
| frameRate   | _object_ | A FrameRate object     |
| timeDisplay | _object_ | A TimeDisplay object   |

#### Returns

| Name     | Type     | Description            |
| :------- | :------- | :----------------------- |
| timecode | _string_ | The timecode string      |

```javascript
const app = require("mediaencoder");
const timecode = app.TickTime.timeToTimecode(time, frameRate, timeDisplay);
timecode; // "00:00:01:00"
```

<HorizontalLine />

### equals

**Instance method.** Checks whether this `TickTime` is equal to another.

Since: **26.5**

#### Parameters

| Name     | Type     | Description                 |
| :------- | :------- | :---------------------------- |
| tickTime | _object_ | The `TickTime` to compare against |

#### Returns

| Name   | Type      | Description                       |
| :----- | :-------- | :---------------------------------- |
| result | _boolean_ | `true` if the two values are equal |

```javascript
const app = require("mediaencoder");
const a = app.TickTime.createWithSeconds(1);
const b = app.TickTime.createWithSeconds(1);
a.equals(b); // true
```

<HorizontalLine />

### toFrame

**Instance method.** Converts this `TickTime` to a frame number at the given frame rate.

Since: **26.5**

#### Parameters

| Name      | Type     | Description         |
| :-------- | :------- | :--------------------- |
| frameRate | _object_ | A FrameRate object     |

#### Returns

| Name  | Type     | Description        |
| :---- | :------- | :-------------------- |
| frame | _number_ | The resulting frame number |

```javascript
const app = require("mediaencoder");
const time = app.TickTime.createWithSeconds(1);
time.toFrame(frameRate);
```

<HorizontalLine />

### alignToNearestFrame

**Instance method.** Aligns this `TickTime` to the nearest frame boundary at the given frame rate.

Since: **26.5**

#### Parameters

| Name      | Type     | Description       |
| :-------- | :------- | :------------------- |
| frameRate | _object_ | A FrameRate object   |

#### Returns

| Name     | Type     | Description                    |
| :------- | :------- | :-------------------------------- |
| tickTime | _object_ | The aligned `TickTime`           |

```javascript
const app = require("mediaencoder");
const time = app.TickTime.createWithSeconds(1.02);
time.alignToNearestFrame(frameRate);
```

<HorizontalLine />

### alignToFrame

**Instance method.** Aligns this `TickTime` to a frame boundary at the given frame rate by flooring.

Since: **26.5**

#### Parameters

| Name      | Type     | Description       |
| :-------- | :------- | :------------------- |
| frameRate | _object_ | A FrameRate object   |

#### Returns

| Name     | Type     | Description             |
| :------- | :------- | :------------------------ |
| tickTime | _object_ | The aligned `TickTime`  |

```javascript
const app = require("mediaencoder");
const time = app.TickTime.createWithSeconds(1.02);
time.alignToFrame(frameRate);
```

<HorizontalLine />

### add

**Instance method.** Adds another `TickTime` to this one.

Since: **26.5**

#### Parameters

| Name     | Type     | Description        |
| :------- | :------- | :-------------------- |
| tickTime | _object_ | The `TickTime` to add |

#### Returns

| Name     | Type     | Description       |
| :------- | :------- | :------------------- |
| tickTime | _object_ | The resulting `TickTime` |

```javascript
const app = require("mediaencoder");
const a = app.TickTime.createWithSeconds(1);
const b = app.TickTime.createWithSeconds(2);
a.add(b); // TickTime representing 3 seconds
```

<HorizontalLine />

### subtract

**Instance method.** Subtracts another `TickTime` from this one.

Since: **26.5**

#### Parameters

| Name     | Type     | Description             |
| :------- | :------- | :------------------------- |
| tickTime | _object_ | The `TickTime` to subtract |

#### Returns

| Name     | Type     | Description       |
| :------- | :------- | :------------------- |
| tickTime | _object_ | The resulting `TickTime` |

```javascript
const app = require("mediaencoder");
const a = app.TickTime.createWithSeconds(3);
const b = app.TickTime.createWithSeconds(1);
a.subtract(b); // TickTime representing 2 seconds
```

<HorizontalLine />

### multiply

**Instance method.** Multiplies this `TickTime` by a factor.

Since: **26.5**

#### Parameters

| Name   | Type     | Description        |
| :----- | :------- | :-------------------- |
| factor | _number_ | The factor to multiply by |

#### Returns

| Name     | Type     | Description       |
| :------- | :------- | :------------------- |
| tickTime | _object_ | The resulting `TickTime` |

```javascript
const app = require("mediaencoder");
const time = app.TickTime.createWithSeconds(1);
time.multiply(2); // TickTime representing 2 seconds
```

<HorizontalLine />

### divide

**Instance method.** Divides this `TickTime` by a divisor.

Since: **26.5**

#### Parameters

| Name    | Type     | Description         |
| :------ | :------- | :--------------------- |
| divisor | _number_ | The divisor to divide by |

#### Returns

| Name     | Type     | Description       |
| :------- | :------- | :------------------- |
| tickTime | _object_ | The resulting `TickTime` |

```javascript
const app = require("mediaencoder");
const time = app.TickTime.createWithSeconds(2);
time.divide(2); // TickTime representing 1 second
```

<HorizontalLine />
