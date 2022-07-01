<template>
  <el-button  @click="dialogFormVisible = true"
  > + new person </el-button
  >
  <el-dialog  v-model="dialogFormVisible" title="information">
  <el-form     :label-position="labelPosition" :model="formLabelAlign" >
    <el-form-item   label="firstName">
      <el-input type="formLabelAlign.firstName"  v-model="formLabelAlign.firstName"/>

    </el-form-item>
    <el-form-item   label="lastName">
      <el-input  type="formLabelAlign.lastName"  v-model="formLabelAlign.lastName" />
    </el-form-item>
    <el-form-item   label="city">
      <el-input  type="formLabelAlign.city" v-model="formLabelAlign.city"/>
    </el-form-item>


  </el-form>
    <template #footer>
      <span class="dialog-footer">
        <el-button @click="dialogFormVisible = false">Cancel</el-button>
        <el-button onsubmit="http://localhost:5000/user/" type="primary" @click="dialogFormVisible = false"
        >Confirm</el-button
        >
      </span>
    </template>
  </el-dialog>

  <el-table  :data="products"
             border
             style="width: 100%">


    <el-table-column  prop="firstName" label="firstName"  >

    </el-table-column>
    <el-table-column prop="lastName" label="lastName" >

    </el-table-column>
    <el-table-column prop="city" label="city" >

    </el-table-column>

  </el-table>


</template>

<script >

import axios from 'axios';
import { ref } from "vue";
import { onMounted } from 'vue'








export default  {
  props: {
    message: String
  },


  setup() {



    const dialogFormVisible = ref(false)
    const labelPosition = ref('left')
    const onSubmit = () => {
      console.log('submit!')
    }
    const formLabelAlign = ref({
      firstName:'deniz' ,
      lastName:'yunsel',
      city:'turkey',
    })

console.log(formLabelAlign.value.firstName)
    const products = ref([]);
    onMounted(() => {
      getProducts();
    })
    onMounted(() => {
      postProducts();
    })





    function getProducts(){

      axios.get('http://localhost:5000/user')
          .then(response => {

           products.value=response.data;


          }).catch(error => {
        console.log(error.response.data);

      });

    }
    function postProducts() {
      axios.post('http://localhost:5000/user/', formLabelAlign.value).then(res => {
        console.log(res.data)
        console.log(formLabelAlign.value.firstName)



      });
    }




    return { products,labelPosition ,formLabelAlign,onSubmit,dialogFormVisible};
  },










};
</script>
<style scoped>
.el-button--text {
  margin-right: 15px;
}
.el-select {
  width: 300px;
}
.el-input {
  width: 300px;
}
.dialog-footer button:first-child {
  margin-right: 10px;
}
</style>