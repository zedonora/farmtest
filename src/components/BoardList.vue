<template>
  <b-row>
    <b-col cols="12">
      <h2>
        Board List
        <b-link href="#/add-board">(Add Board)</b-link>
      </h2>
      <b-table striped hover :items="boards" :fields="fields">
        <template slot="actions" scope="row">
          <b-btn size="sm" @click.stop="details(row.item)">Details</b-btn>
        </template>
      </b-table>
    </b-col>
  </b-row>
</template>

<script>
import firebase from "../Firebase";
import router from "../router";

export default {
  name: "BoardList",
  data() {
    return {
      fields: {
        title: { label: "Title", sortable: true, class: "text-left" },
        collectDate: {
          label: "주문수집일시",
          sortable: true,
          class: "text-left"
        },
        orderState: {
          label: "주문상태",
          sortable: true,
          class: "text-left"
        },
        shopNmae: {
          label: "쇼핑몰",
          sortable: true,
          class: "text-left"
        },
        orderNumber: {
          label: "주문번호",
          sortable: true,
          class: "text-left"
        },
        productNmae: {
          label: "상품명",
          sortable: true,
          class: "text-left"
        },
        option: {
          label: "옵션",
          sortable: true,
          class: "text-left"
        },
        quantity: {
          label: "수량",
          sortable: true,
          class: "text-left"
        },
        price: {
          label: "주문금액",
          sortable: true,
          class: "text-left"
        },
        recipient: {
          label: "수령인",
          sortable: true,
          class: "text-left"
        },
        cellPhone: {
          label: "수령인휴대폰",
          sortable: true,
          class: "text-left"
        },
        phone: {
          label: "수령인전화번호",
          sortable: true,
          class: "text-left"
        },
        zipCode: {
          label: "우편번호",
          sortable: true,
          class: "text-left"
        },
        address: {
          label: "주소",
          sortable: true,
          class: "text-left"
        },
        shipMessage: {
          label: "배송메세지",
          sortable: true,
          class: "text-left"
        },
        buyer: {
          label: "주문자",
          sortable: true,
          class: "text-left"
        },
        shipNumber: {
          label: "배송번호",
          sortable: true,
          class: "text-left"
        },
        location: {
          label: "로케이션",
          sortable: true,
          class: "text-left"
        },
        actions: { label: "Action", class: "text-center" }
      },
      boards: [],
      errors: [],
      ref: firebase.firestore().collection("boards")
    };
  },
  created() {
    this.ref.onSnapshot(querySnapshot => {
      this.boards = [];
      querySnapshot.forEach(doc => {
        this.boards.push({
          key: doc.id,
          collectDate: doc.data().collectDate,
          orderState: doc.data().orderState,
          shopNmae: doc.data().shopNmae,
          orderNumber: doc.data().orderNumber,
          productNmae: doc.data().productNmae,
          option: doc.data().option,
          quantity: doc.data().quantity,
          price: doc.data().price,
          recipient: doc.data().recipient,
          cellPhone: doc.data().cellPhone,
          phone: doc.data().phone,
          zipCode: doc.data().zipCode,
          address: doc.data().address,
          shipMessage: doc.data().shipMessage,
          buyer: doc.data().buyer,
          shipNumber: doc.data().shipNumber,
          location: doc.data().location
        });
      });
    });
  },
  methods: {
    details(board) {
      router.push({ name: "ShowBoard", params: { id: board.key } });
    }
  }
};
</script>

<style>
.table {
  width: 96%;
  margin: 0 auto;
}
</style>