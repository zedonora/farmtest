<template>
  <b-row>
    <b-col cols="12">
      <h2>
        Add Board
        <b-link href="#/">(Board List)</b-link>
      </h2>
      <b-jumbotron>
        <b-form @submit="onSubmit">
          <b-form-group
            id="fieldsetHorizontal"
            horizontal
            :label-cols="4"
            breakpoint="md"
            label="주문수집일시"
          >
            <b-form-input id="collectDate" v-model.trim="board.collectDate"></b-form-input>
          </b-form-group>
          <b-form-group
            id="fieldsetHorizontal"
            horizontal
            :label-cols="4"
            breakpoint="md"
            label="주문상태"
          >
            <b-form-input id="orderState" v-model.trim="board.orderState"></b-form-input>
          </b-form-group>
          <b-form-group
            id="fieldsetHorizontal"
            horizontal
            :label-cols="4"
            breakpoint="md"
            label="쇼핑몰"
          >
            <b-form-input id="shopNmae" v-model.trim="board.shopNmae"></b-form-input>
          </b-form-group>
          <b-form-group
            id="fieldsetHorizontal"
            horizontal
            :label-cols="4"
            breakpoint="md"
            label="주문번호"
          >
            <b-form-input id="orderNumber" v-model.trim="board.orderNumber"></b-form-input>
          </b-form-group>
          <b-form-group
            id="fieldsetHorizontal"
            horizontal
            :label-cols="4"
            breakpoint="md"
            label="상품명"
          >
            <b-form-input id="productNmae" v-model.trim="board.productNmae"></b-form-input>
          </b-form-group>
          <b-form-group
            id="fieldsetHorizontal"
            horizontal
            :label-cols="4"
            breakpoint="md"
            label="옵션"
          >
            <b-form-input id="option" v-model.trim="board.option"></b-form-input>
          </b-form-group>
          <b-form-group
            id="fieldsetHorizontal"
            horizontal
            :label-cols="4"
            breakpoint="md"
            label="수량"
          >
            <b-form-input id="quantity" v-model.trim="board.quantity"></b-form-input>
          </b-form-group>
          <b-form-group
            id="fieldsetHorizontal"
            horizontal
            :label-cols="4"
            breakpoint="md"
            label="주문금액"
          >
            <b-form-input id="price" v-model.trim="board.price"></b-form-input>
          </b-form-group>
          <b-form-group
            id="fieldsetHorizontal"
            horizontal
            :label-cols="4"
            breakpoint="md"
            label="수령인"
          >
            <b-form-input id="recipient" v-model.trim="board.recipient"></b-form-input>
          </b-form-group>
          <b-form-group
            id="fieldsetHorizontal"
            horizontal
            :label-cols="4"
            breakpoint="md"
            label="수령인휴대폰"
          >
            <b-form-input id="cellPhone" v-model.trim="board.cellPhone"></b-form-input>
          </b-form-group>
          <b-form-group
            id="fieldsetHorizontal"
            horizontal
            :label-cols="4"
            breakpoint="md"
            label="수령인전화번호"
          >
            <b-form-input id="phone" v-model.trim="board.phone"></b-form-input>
          </b-form-group>
          <b-form-group
            id="fieldsetHorizontal"
            horizontal
            :label-cols="4"
            breakpoint="md"
            label="우편번호"
          >
            <b-form-input id="zipCode" v-model.trim="board.zipCode"></b-form-input>
          </b-form-group>
          <b-form-group
            id="fieldsetHorizontal"
            horizontal
            :label-cols="4"
            breakpoint="md"
            label="주소"
          >
            <b-form-input id="address" v-model.trim="board.address"></b-form-input>
          </b-form-group>
          <b-form-group
            id="fieldsetHorizontal"
            horizontal
            :label-cols="4"
            breakpoint="md"
            label="배송메세지"
          >
            <b-form-input id="shipMessage" v-model.trim="board.shipMessage"></b-form-input>
          </b-form-group>
          <b-form-group
            id="fieldsetHorizontal"
            horizontal
            :label-cols="4"
            breakpoint="md"
            label="주문자"
          >
            <b-form-input id="buyer" v-model.trim="board.buyer"></b-form-input>
          </b-form-group>
          <b-form-group
            id="fieldsetHorizontal"
            horizontal
            :label-cols="4"
            breakpoint="md"
            label="배송번호"
          >
            <b-form-input id="shipNumber" v-model.trim="board.shipNumber"></b-form-input>
          </b-form-group>
          <b-form-group
            id="fieldsetHorizontal"
            horizontal
            :label-cols="4"
            breakpoint="md"
            label="로케이션"
          >
            <b-form-input id="location" v-model.trim="board.location"></b-form-input>
          </b-form-group>
          <b-form-group
            id="fieldsetHorizontal"
            horizontal
            :label-cols="4"
            breakpoint="md"
            label="Enter Description"
          >
            <b-form-textarea
              id="description"
              v-model="board.description"
              placeholder="Enter something"
              :rows="2"
              :max-rows="6"
            >{{board.description}}</b-form-textarea>
          </b-form-group>
          <b-button type="submit" variant="primary">Save</b-button>
        </b-form>
      </b-jumbotron>
    </b-col>
  </b-row>
</template>

<script>
import firebase from "../Firebase";
import router from "../router";

export default {
  name: "AddBoard",
  data() {
    return {
      ref: firebase.firestore().collection("boards"),
      board: {}
    };
  },
  methods: {
    onSubmit(evt) {
      evt.preventDefault();

      this.ref
        .add(this.board)
        .then(docRef => {
          this.board.title = "";
          this.board.description = "";
          this.board.author = "";
          router.push({
            name: "BoardList"
          });
        })
        .catch(error => {
          alert("Error adding document: ", error);
        });
    }
  }
};
</script>

<style>
.jumbotron {
  padding: 2rem;
}
</style>