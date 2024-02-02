<template>
  <table id="list">
    <tr>
      <td>글제목</td>
      <td><input type="text" v-model="title"></td>
    </tr>
    <tr>
      <td colspan="2">
        <textarea v-model="content"></textarea>
      </td>
    </tr>
  </table>
  <button style="float: right;" @click="boardSave">저장</button>
</template>

<script>
export default {
  data() {
    return {
      title: '',
      content: ''
    }
  },
  methods: {
    boardSave() {
      // 순서대로 파라미터가 넘어감.
      this.$emit('save-board', this.title, this.content); // 부모컴포넌트에게 메소드 실행 요청.
    }
  }
}
</script>