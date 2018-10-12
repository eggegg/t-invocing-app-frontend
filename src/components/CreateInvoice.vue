<template>
  <div>
    <div class="container">
      <div class="tab-pane fade show active">
          <div class="row">
              <div class="col-md-12">
                  <h3>Enter Details below to Create Invoice</h3>
                  <form @submit.prevent="onSubmit">
                      <div class="form-group">
                          <label for="">Invoice Name:</label>
                          <input type="text" required class="form-control" placeholder="eg Seller's Invoice" v-model="invoice.name">
                      </div>
                      <div class="form-group">
                          <button class="btn btn-primary" >Create Invoice</button>
                          {{ loading }}
                          {{ status }}
                      </div>
                  </form> 
              </div>
          </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "CreateInvoice",
  components: {},
  data() {
    return {
      invoice: {
        name: "",
      },
      loading: "",
      status: ""
    };
  },
  methods: {
    
    onSubmit() {
      const formData = new FormData();
     
      formData.append("name", this.invoice.name);
      
      let user = JSON.parse(localStorage.getItem('user'));
      
      this.loading = "Creating Invoice, please wait ...";
      // Post to server
      axios.post("http://localhost:8080/invoice", formData, {
        headers: {"Authorization": "Bearer " + localStorage.getItem("token")}
      }).then(res => {
        // Post a status message
        this.loading = "";
        if (res.data.status == true) {
          this.status = res.data.message;
        } else {
          this.status = res.data.message;
        }
      });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #426cb9;
}
.tab-pane {
  margin-top: 20px;
}
</style>