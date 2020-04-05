# react-number-format

### Install

```react
npm install react-number-format --save
```

### Usage

```
import NumberFormat from 'react-number-format';
```

### Examples

#### Format mata uang :

```
var NumberFormat = require('react-number-format');

<NumberFormat value={2456981} displayType={'text'} thousandSeparator={true} prefix={'Rp.'} renderText
```

Output : <div> Rp.2,456,981 </div>

#### Format credit card :

```
<NumberFormat format="+62 (###) ###-####" mask="_"/>
```

#### Format credit card :

```
<NumberFormat format="#### #### #### ####" mask="_"/>
```