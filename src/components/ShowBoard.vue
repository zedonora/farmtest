<template>
  <b-row>
    <b-col cols="12">
      <h2>
        Edit Board
        <b-link href="#/">(Board List)</b-link>
      </h2>
      <b-jumbotron>
        <template slot="header">{{board.title}}</template>
        <template slot="lead">
          주문수집일시: {{board.collectDate}}
          <br>
          주문상태: {{board.orderState}}
          <br>
          쇼핑몰: {{board.shopNmae}}
          <br>
          주문번호: {{board.orderNumber}}
          <br>
          상품명: {{board.productNmae}}
          <br>
          옵션: {{board.option}}
          <br>
          수량: {{board.quantity}}
          <br>
          주문금액: {{board.price}}
          <br>
          수령인: {{board.recipient}}
          <br>
          수령인휴대폰: {{board.cellPhone}}
          <br>
          수령인전화번호: {{board.phone}}
          <br>
          우편번호: {{board.zipCode}}
          <br>
          주소: {{board.address}}
          <br>
          배송메세지: {{board.shipMessage}}
          <br>
          주문자: {{board.buyer}}
          <br>
          배송번호: {{board.shipNumber}}
          <br>
          로케이션: {{board.location}}
          <br>
        </template>
        <hr class="my-4">
        <b-btn class="edit-btn" variant="success" @click.stop="editboard(key)">Edit</b-btn>
        <b-btn variant="danger" @click.stop="deleteboard(key)">Delete</b-btn>
      </b-jumbotron>
    </b-col>
  </b-row>
</template>

<script>
import firebase from "../Firebase";
import router from "../router";

export default {
  name: "ShowBoard",
  data() {
    return {
      key: "",
      board: {}
    };
  },
  created() {
    const ref = firebase
      .firestore()
      .collection("boards")
      .doc(this.$route.params.id);
    ref.get().then(doc => {
      if (doc.exists) {
        this.key = doc.id;
        this.board = doc.data();
      } else {
        alert("No such document!");
      }
    });
  },
  methods: {
    editboard(id) {
      router.push({
        name: "EditBoard",
        params: { id: id }
      });
    },
    deleteboard(id) {
      firebase
        .firestore()
        .collection("boards")
        .doc(id)
        .delete()
        .then(() => {
          router.push({
            name: "BoardList"
          });
        })
        .catch(error => {
          alert("Error removing document: ", error);
        });
    }
  }
};
</script>

<style>
.jumbotron {
  padding: 2rem;
}
.edit-btn {
  margin-right: 20px;
  width: 70px;
}
</style>