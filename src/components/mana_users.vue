<template>
  <div class="container">
      <div class="title_pageproducts">
          <div class="text_title">
              Tất cả người dùng
          </div>
      </div>
      <div class="row">
          <div class="col-12" style="border: solid 1px #aaa;">
              <table class="table">
                  <thead>
                      <tr>
                      <th scope="col"></th>
                      <th scope="col">Người dùng</th>
                      <th scope="col">Tên người dùng</th>
                      <th scope="col">Email</th>
                      <th sopce="col">Địa chỉ</th>
                      <th scope="col">Số điện thoại</th>
                      <th scope="col">Vai trò</th>
                      </tr>
                  </thead>
                  <tbody class="table-group-divider">
                      <list_cardmana v-for="product in cart" :key="product.id" :products="product" />
                  </tbody>
              </table>
          </div>
      </div>
      <div style="height: 300px"></div>
  </div>
</template>

<script>
import list_cardmana from './partials/admin_partials/list_usersmana.vue';

export default {
  data: () => ({
    loading: false,
  }),
  data(){
    return{
      cart:[],
      totalprice: 0
    }
  },
  async mounted(){

    const ress = await axios.get('http://localhost:3000/user/getall');
    this.cart = ress.data
    console.log(this.cart)
  
  },
  watch: {
    loading (val) {
      if (!val) return

      setTimeout(() => (this.loading = false), 2000)
    },
  },
  components:{
    list_cardmana
  },
  prop:{
    listproducts:{
          type: Array,
          default: []
      }
  },
  methods:{
    toVND(x){
    return new Intl.NumberFormat('vi-VN', { style: 'currency', currency: 'VND' }).format(x)
  },
  }
}
</script>

<style scoped>
.title_pageproducts{
width: 100%;
height: 100px;
}
.text_title{
text-align: center;
font-size: 50px;
font-family: 'Josefin_Sans';
font-weight: 300;
padding: 14px;
}
.title_total{
text-align: start;
font-size: 30px;
font-family: 'Josefin_Sans';
font-weight: 300;
padding: 14px;
}
.container_total{
  width: 98%;
  height: 150px;
  border: solid 1px #aaa;
}
.ctner{
  width: 98%;
  height: 400px;
}
.cusbtn{
  background-color: #ebebeb;
  font-family: 'Josefin_Sans';
}
.imagee{
  width: 100px;
  height: 100px;
}
</style>
