<template>
  <main className="mt-3">
    <div className="container">
      <h2 className="text-center">제품 수정</h2>
      <div className="mb-3 row">
        <label className="col-sm-3 col-form-label">제품명</label>
        <div className="col-md-9">
          <input type="text" className="form-control" v-model="productDetail.product_name">
        </div>
      </div>
      <div className="mb-3 row">
        <label className="col-sm-3 col-form-label">제품가격</label>
        <div className="col-md-9">
          <div className="input-group mb-3">
            <input type="number" className="form-control" v-model="productDetail.product_price">
            <span className="input-group-text">원</span>
          </div>
        </div>
      </div>
      <div className="mb-3 row">
        <label className="col-sm-3 col-form-label">배송비</label>
        <div className="col-md-9">
          <div className="input-group mb-3">
            <input type="number" className="form-control" v-model="productDetail.delivery_price">
            <span className="input-group-text">원</span>
          </div>
        </div>
      </div>
      <div className="mb-3 row">
        <label className="col-md-3 col-form-label">추가배송비(도서산간)</label>
        <div className="col-md-9">
          <div className="input-group mb-3">
            <input type="number" className="form-control" v-model="productDetail.add_delivery_price">
            <span className="input-group-text">원</span>
          </div>
        </div>
      </div>
      <div className="mb-3 row">
        <label className="col-md-3 col-form-label">제품카테고리</label>
        <div className="col-md-9">
          <div className="row">
            <div className="col-auto">
              <select className="form-select">
                <option>전자제품</option>
              </select>
            </div>
            <div className="col-auto">
              <select className="form-select">
                <option>컴퓨터</option>
              </select>
            </div>
            <div className="col-auto">
              <select className="form-select">
                <option>악세사리</option>
              </select>
            </div>
          </div>
        </div>
      </div>
      <div className="mb-3 row">
        <label className="col-sm-3 col-form-label">태그</label>
        <div className="col-md-9">
          <input type="text" className="form-control" v-model="productDetail.tags">
        </div>
      </div>
      <div className="mb-3 row">
        <label className="col-sm-3 col-form-label">출고일</label>
        <div className="col-md-9">
          <div className="input-group mb-3">
            <input type="number" className="form-control" v-model="productDetail.outbound_days">
            <span className="input-group-text">일 이내 출고</span>
          </div>
        </div>
      </div>
      <div className="mb-3 row">
        <div className="col-6 d-grid p-1">
          <button type="button" className="btn btn-lg btn-dark"  @click="gotoList">취소하기</button>
        </div>
        <div className="col-6 d-grid p-1">
          <button type="button" className="btn btn-lg btn-danger">저장하기</button>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      productId: 0,
      productDetail: []
    }
  },
  computed: {
    user() {
      return this.$store.state.user;
    }
  },
  mounted() {
    if(this.user.email == undefined) {
      alert("로그인을 해야 이용할 수 있습니다.");
      this.$router.push({path:'/'});
    }
  },
  created() {
    this.productId = this.$route.query.product_id;
    this.getProductDetail();
  },
  methods: {
    gotoList(){
      this.$router.push({path:'/sales'});
    },
    async getProductDetail() {
      let productDetail = await this.$api("/api/productDetail", {param:[this.productId]});
      if(productDetail.length > 0) {
        this.productDetail = productDetail[0];
      }
    }
  }
}

</script>