# promise

```js


```
# promise.then
# promise.all

```js
promise().MyAll = function(promises){

	let resolve, reject

	const p = new promise((resolve, reject) => {
		resolve = resolve
		reject = reject
	})
	
	// 判断空数组情况
	let count = 0
	let i = 0
	let fullfilledCount = 0
	const result = []
	for (const prom of promises){
		count++
		const index = i
		i++
		Promise.resolve(prom).then(
		(date) => {
			// 1.收集所有结果
			fullfilledCount++
			result[index] = date
			// 2.触发MyAll的状态改变
			if(fullfilledCount === count){
				resolve(result)
			}
		},
		() => {
			reject
		}
		)
	}
	if(count === 0){
		resolve(result)
	}

	return p

}
```
