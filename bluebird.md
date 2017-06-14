### bluebird

- 비동기 Promise개념을 향상시킴 (JavaScript의 Promise)
- `new Promise(function(function resolve, function reject) resolver) -> Promise`
- .then
	- 정상적인 마무리후 rosolve
- .catch
	- error handling
- .spread
	- return 값이 다름
	- then과 비슷

```
Promise.all([
  new Promise(function(resolve, reject){
    ....
    if(err) reject(err);
    else resolve(result1);
  },
  new Promise(function(resolve, reject){
    ....
    if(err) reject(err);
    else resolve(result2);
  }
]).then(function(result){
  var result1 = result[0];
  var result2 = result[1];
  ....
});
```
```Promise.all([
  new Promise(function(resolve, reject){
    ....
    if(err) reject(err);
    else resolve(result1);
  },
  new Promise(function(resolve, reject){
    ....
    if(err) reject(err);
    else resolve(result2);
  }
]).spread(function(result1, result2){
  console.log(result1);
  console.log(result2);
  ....
});
```

- .finally
	- 무조건 마지막에 실행
	- 에러가 있어도 실행

- .bind
	- .bind를 사용하면 변수를 일부러 선언 할 필요없이 .bind를 사용한 함수 내에서 변수의 사용이 자유롭다.

```
var scope = {};
somethingAsync().spread(function (aValue, bValue) {
  scope.aValue = aValue;
  scope.bValue = bValue;
  return somethingElseAsync(aValue, bValue);
}).then(function (cValue) {
  return scope.aValue + scope.bValue + cValue;
});
```

```
somethingAsync().bind({}).spread(function (aValue, bValue) {
    this.aValue = aValue;
    this.bValue = bValue;
    return somethingElseAsync(aValue, bValue);
}).then(function (cValue) {
    return this.aValue + this.bValue + cValue;
});
```