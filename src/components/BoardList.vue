<template>
  <div>
    <table id="list">
      <thead>
        <tr>
          <th>글번호</th>
          <th>글제목</th>
          <th>조회</th>
          <th>삭제</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="board in list" v-bind:key="board.no">
          <td>{{board.no}}</td>
          <td @click="showRead(board)">{{board.title}}</td>
          <td>{{board.view}}</td>
          <td><button @click="deleteBoard(board.no)">삭제</button></td>
        </tr>
      </tbody>
    </table>
    <button style="float: right;" @click="showWrite">글쓰기</button>
  </div>
</template>

<script>
export default {
  props: ['list'], // 부모 컴포넌트의 전달 값을 받는 속성.
  data () {
    return {

    }
  },
  methods: {
    showWrite() {  // 자식 컴포넌트는 부모 컴포넌트에 값을 바꿔달라고 요청함.
      console.log(this.$parent);
      // 부모컴포넌트 데이터를 변경.

      // 이렇게 하면 나중에 불편함.
      // this.$parent.listView = false;
      // this.$parent.writeView = true;
      
      // 이렇게 해라.
      this.$emit('show-write'); // 부모컴포넌트의 이벤트를 실행하기위한 호출.
    },
    showRead(board) {
      // 상세화면 보여주기.
      this.$emit('show-read', board);
    },
    deleteBoard(no) {
      this.$emit('delete-board', no);
    }
  }
}
</script>
