<template>
  <div class="customers container">
    <Alert v-if="alert" v-bind:message="alert"></Alert>
    <h1 class="page-header">用户管理系统</h1>
    <input type="text" class="form-control search" placeholder="搜索" v-model="filterInput">
    <table class="table table-striped">
      <thead>
        <tr>
          <th>姓名</th>
          <th>学校</th>
          <th>学历</th>
          <th>电话</th>
          <!-- <th>邮箱</th> -->
          <th>操作</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="customer in filterBy(customers,filterInput)" :key="customer.id">
          <td>{{customer.name}}</td>
          <td>{{customer.graduationschool}}</td>
          <td>{{customer.profession}}</td>
          <td>{{customer.phone}}</td>
          <!-- <td>{{customer.email}}</td> -->
          <td><router-link class="btn btn-default" v-bind:to="'/customer/' + customer.id">详情</router-link></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import Alert from './Alert'
export default {
  name: 'customers',
  data () {
    return {
      customers: [],
      alert: '',
      filterInput: ''
    }
  },
  methods: {
    fetchCustomers () {
      this.$http.get('http://localhost:3000/users')
        .then(function (response) {
          // console.log(response)
          this.customers = response.body
        })
    },
    filterBy (customers, value) {
      return customers.filter(function (customer) {
        return customer.name.match(value)
      })
    }
  },
  created () {
    if (this.$route.query.alert) {
      this.alert = this.$route.query.alert
    }
    this.fetchCustomers()
  },
  updated () {
    // this.fetchCustomers()
  },
  components: {
    Alert
  }
}
</script>

<style scoped>
h1 {
  font-size: 30px;
}
.search {
  background: #F1F3F4;
  margin-bottom: 10px;
}
.bar6 input {
  border: 2px solid #222;
  border-radius: 5px;
  background: transparent;
  top: 0;
  right: 0;
}
.bar6 button {
  background: #222;
  border-radius: 0 5px 5px 0;
  width: 60px;
  top: 0;
  right: 0;
}
.bar6 button:before {
  content: "搜索";
  font-size: 13px;
  color: #f9f0da;
}
</style>
