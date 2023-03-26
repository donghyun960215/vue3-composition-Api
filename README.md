# 컴포지션 API

## 컴포지션 API
```html
<template>
  <h1 @click="increase">
    {{ count }} / {{ doubleCount }}
  </h1>
  <h1>
    {{ message }} / {{ reversedMessage }}
  </h1>
</template>

<script>


export default {
  data() {
    return {
      message: 'Hello world',
      count: 0
    }
  },
  computed: {
    doubleCount() {
      return this.count *2
    },
    reversedMessage() {
      return this.message.split('').reverse().join('')
    }
  },
  methods: {
    increase() {
      this.count += 1
    }
  }
}
</script>
```
```plaintext
기존작성법대로 작성을 하면 위와 같이 작성을 할 수 있다. 
로직을 살펴보면 count 와 message 부분이 섞여 있는걸 볼 수 있다.
지금은 로직이 간단해서 문제 없이 볼 수 있지만 복잡해 진다면 로직을 보는게 어려워진다.
```

```html
<template>
  <h1 @click="increase">
    {{ count }} / {{ doubleCount }}
  </h1>
  <h1>
    {{ message }} / {{ reversedMessage }}
  </h1>
</template>

<script>
import { ref, computed } from 'vue'


export default {
  setup() {
    const message = ref('Hello world')
    const reversedMessage = computed(() => {
      return message.value.split('').reverse().join('')
    })

    const count = ref(0)
    const doubleCount = computed(() => count.value * 2 )
    function increase() {
      count.value += 1
    }

    return{
      message,
      reversedMessage,
      count,
      doubleCount,
      increase
    }
  }
}
</script>
```
```plaintext
컴포지션API를 사용하여 위와 같이 작성을 할 수 있다.
```

## 반응형 데이터(반응성)
### 반응성 없음
```html
<template>
  <div @click="increase">
    {{ count }}
  </div>
</template>

<script>
export default {
  setup() {
    let count = 0
    function increase() {
      count += 1
    }

    return{
      count,
      increase
    }
  }
}
</script>
```
```plaintext
위 와 같이 작성을 하면 작성단계는 문제는 없지만 반응성이 없다.
```
### 반응성 있음
```html
<template>
  <div @click="increase">
    {{ count }}
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  setup() {
    let count = ref(0)
    function increase() {
      count.value += 1
    }

    return{
      count,
      increase
    }
  }
}
</script>
```
```plaintext
ref() 함수를 실행을 해서 그 안에 초기값을 지정해주고 그렇게 해주면 count에는 하나의 객체데이터가 반환이된다.
그러면 count를 데이터로 직접 사용을 할 수 없고 count라는 객체데이터 내부에 value라는 속성을 사용한다.
컴포지션 API에서 반응성을 가진 데이터를 사용하기 위해서는 vue패키지에서 ref를 가져와서 사용한다.
```