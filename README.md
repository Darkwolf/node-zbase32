# ZBase32
## Install
`npm i --save @darkwolf/zbase32`
## Usage
```javascript
// ECMAScript
import ZBase32 from '@darkwolf/zbase32'
// CommonJS
const ZBase32 = require('@darkwolf/zbase32')

// Number Encoding
const integer = Number.MAX_SAFE_INTEGER // => 9007199254740991
const encodedInt = ZBase32.encodeInt(integer) // => '89999999999'
const decodedInt = ZBase32.decodeInt(encodedInt) // => 9007199254740991

const negativeInteger = -integer // => -9007199254740991
const encodedNegativeInt = ZBase32.encodeInt(negativeInteger) // => '-89999999999'
const decodedNegativeInt = ZBase32.decodeInt(encodedNegativeInt) // => -9007199254740991

// BigInt Encoding
const bigInt = BigInt(Number.MAX_VALUE) // => 179769313486231570814527423731704356798070567525844996598917476803157260780028538760589558632766878171540458953514382464234321326889464182768467546703537516986049910576551282076245490090389328944075868508455133942304583236903222948165808559332123348274797826204144723168738177180919299881250404026184124858368n
const encodedBigInt = ZBase32.encodeBigInt(bigInt) // => 'x9999999996yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy'
const decodedBigInt = ZBase32.decodeBigInt(encodedBigInt) // => 179769313486231570814527423731704356798070567525844996598917476803157260780028538760589558632766878171540458953514382464234321326889464182768467546703537516986049910576551282076245490090389328944075868508455133942304583236903222948165808559332123348274797826204144723168738177180919299881250404026184124858368n

const negativeBigInt = -bigInt // => -179769313486231570814527423731704356798070567525844996598917476803157260780028538760589558632766878171540458953514382464234321326889464182768467546703537516986049910576551282076245490090389328944075868508455133942304583236903222948165808559332123348274797826204144723168738177180919299881250404026184124858368n
const encodedNegativeBigInt = ZBase32.encodeBigInt(negativeBigInt) // => '-x9999999996yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy'
const decodedNegativeBigInt = ZBase32.decodeBigInt(encodedNegativeBigInt) // => -179769313486231570814527423731704356798070567525844996598917476803157260780028538760589558632766878171540458953514382464234321326889464182768467546703537516986049910576551282076245490090389328944075868508455133942304583236903222948165808559332123348274797826204144723168738177180919299881250404026184124858368n

// Text Encoding
const text = 'Ave, Darkwolf!'
const encodedText = ZBase32.encodeText(text) // => 'ef5gkmbyetozr45zp7sgcee'
const decodedText = ZBase32.decodeText(encodedText) // => 'Ave, Darkwolf!'

const emojis = '🐺🐺🐺'
const encodedEmojis = ZBase32.encodeText(emojis) // => '6nx3bqzou6emihr91n7y'
const decodedEmojis = ZBase32.decodeText(encodedEmojis) // => '🐺🐺🐺'

// Buffer Encoding
const buffer = Uint8Array.of(0x00, 0x02, 0x04, 0x08, 0x0f, 0x1f, 0x3f, 0x7f, 0xff) // => <Uint8Array 00 02 04 08 0f 1f 3f 7f ff>
const encodedBuffer = ZBase32.encode(buffer) // => <Uint8Array 79 79 62 79 65 6e 79 78 64 68 39 7a 39 39 61>
const decodedBuffer = ZBase32.decode(encodedBuffer) // => <Uint8Array 00 02 04 08 0f 1f 3f 7f ff>

const encodedBufferToString = ZBase32.encodeToString(buffer) // => 'yybyenyxdh9z99a'
const decodedBufferFromString = ZBase32.decodeFromString(encodedBufferToString) // => <Uint8Array 00 02 04 08 0f 1f 3f 7f ff>

// Custom Alphabet
const zbase32 = new ZBase32('13456789abcdefghijkmnopqrstuwxyz')

const encInt = zbase32.encodeInt(integer) // => '9zzzzzzzzzz'
const decInt = zbase32.decodeInt(encInt) // => 9007199254740991

const encNegativeInt = zbase32.encodeInt(negativeInteger) // => '-9zzzzzzzzzz'
const decNegativeInt = zbase32.decodeInt(encNegativeInt) // => -9007199254740991

const encBigInt = zbase32.encodeBigInt(bigInt) // 'hzzzzzzzzzy11111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111'
const decBigInt = zbase32.decodeBigInt(encBigInt) // => 179769313486231570814527423731704356798070567525844996598917476803157260780028538760589558632766878171540458953514382464234321326889464182768467546703537516986049910576551282076245490090389328944075868508455133942304583236903222948165808559332123348274797826204144723168738177180919299881250404026184124858368n

const encNegativeBigInt = zbase32.encodeBigInt(negativeBigInt) // => '-hzzzzzzzzzy11111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111'
const decNegativeBigInt = zbase32.decodeBigInt(encNegativeBigInt) // => -179769313486231570814527423731704356798070567525844996598917476803157260780028538760589558632766878171540458953514382464234321326889464182768467546703537516986049910576551282076245490090389328944075868508455133942304583236903222948165808559332123348274797826204144723168738177180919299881250404026184124858368n

const encText = zbase32.encodeText(text) // => 'a7u8cd31ajiq6tuqfxp8eaa'
const decText = zbase32.decodeText(encText) // => 'Ave, Darkwolf!'

const encEmojis = zbase32.encodeText(emojis) // => 'y4hs3gqimyadow6zk4x1'
const decEmojis = zbase32.decodeText(encEmojis) // => '🐺🐺🐺'

const encBuffer = zbase32.encode(buffer) // => <Uint8Array 31 31 33 31 61 34 31 68 35 77 7a 71 7a 7a 72>
const decBuffer = zbase32.decode(encBuffer) // => <Uint8Array 00 02 04 08 0f 1f 3f 7f ff>

const encBufferToString = zbase32.encodeToString(buffer) // => '1131a41h5wzqzzr'
const decBufferFromString = zbase32.decodeFromString(encBufferToString) // => <Uint8Array 00 02 04 08 0f 1f 3f 7f ff>
```
## [API Documentation](https://github.com/Darkwolf/node-zbase32/blob/master/docs/API.md)
## Contact Me
#### GitHub: [@PavelWolfDark](https://github.com/PavelWolfDark)
#### Telegram: [@PavelWolfDark](https://t.me/PavelWolfDark)
#### Email: [PavelWolfDark@gmail.com](mailto:PavelWolfDark@gmail.com)
