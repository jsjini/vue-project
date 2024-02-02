<template>
  <header>
    <h2>간단 게시판</h2>
    <p>뷰로 작성하는 게시판</p>
  </header>
  <p>{{ rootList }}</p>
  <p>{{ rootStr }}</p>
</template>

<script>
export default {
  props: ['rootData'], // 바로 상위(부모)컨포넌트에는 데이터 받을 수 있지만 조상급은 안됨.
  // 조상급은 Provide/Inject 사용해야 데이터 전달 가능 (읽기 전용...)
  inject: ['rootList', 'rootStr']
}
</script>