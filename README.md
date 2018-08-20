![Alt text](http://p5qgrn52w.bkt.clouddn.com/autocomplete/%E5%BD%95%E5%88%B6_2018_08_20_14_31_59_699.gif)

安装
```
npm i -save autocomplete-puge
或
yarn add autocomplete-puge
```

使用
```
<template>
  <div>
    <Autocomplete @change="inputChange"></Autocomplete>
  </div>
</template>

<script>
import Autocomplete from 'autocomplete-puge'
export default {
  components: {
    Autocomplete
  },
  methods: {
    inputChange (e) {
      console.log(e)
    }
  }
}
</script>
```

## 事件

| 参数        | 含义         | 类型  |
| ----------- |:-------------:| -----:|
|change| 输入内容发生改变 | event |
