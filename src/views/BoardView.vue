<template>
  <div>
    <HeaderComponent />
    <BoardList v-if="listView" v-bind:list="boardList" @show-write="showWrite" @delete-board="deleteBoard" @show-read="showRead" />
    <BoardWrite v-if="writeView" @save-board="saveBoard" />
    <BoardRead v-if="readView" v-bind:board="board" @show-list="showList"/>
    <!--html 전달-->
    <FooterComponent v-bind:data="htmlData">
      <template v-slot:footer><p>Since 2020</p></template>
      <template v-slot:header><h3>Header 들어갈 내용</h3></template>
      <template v-slot:default><p>Hello, World</p></template>
    </FooterComponent>
  </div>
</template>

<script>
import BoardList from '../components/BoardList.vue'
import HeaderComponent from '../components/HeaderComponent.vue'
import FooterComponent from '../components/FooterComponent.vue'
import BoardWrite from '../components/BoardWrite.vue'
import BoardRead from '../components/BoardRead.vue'

export default {
  data () {
    return {
      listView: true,
      writeView: false,
      readView: false,
      board: {}, // 상세화면에 사용할 데이터.
      boardList: [
        { no: 1, title: 'Vue는 좋아요', content: '프레임워크입니다', view: 1 },
        { no: 2, title: '좋은 아침입니다', content: '금요일이네요', view: 3 }
      ],
      htmlData: '<p>Hello</p>'
    }
  },
  components: {
    BoardList,
    HeaderComponent,
    FooterComponent,
    BoardWrite,
    BoardRead
  },
  methods: {
    showWrite() { // 등록화면을 보여주는기능.
      this.listView = false;
      this.writeView = true;
    },
    showList() {
      this.listView = true;
      this.writeView = false;
      this.readView = false;
    },
    showRead(board) {  // 상세화면
      board.view++;
      this.board = board;
      this.listView = false;
      this.readView = true;
    },
    saveBoard(title, content) {
      let idx = this.boardList.length - 1;
      let no = parseInt(this.boardList[idx].no) + 1;
      let board = {no, title, content, view: 0};
      this.boardList.push(board);
      this.showList();
    },
    deleteBoard(no) {
      this.boardList = this.boardList.filter(board => board.no == no ? false : true);
    }
  }
}
</script>
