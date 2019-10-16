<template>
  <div class="details container">
    <router-link class="btn btn-default" to="/">返回</router-link>
      <h1 class="page-header">
        {{customer.name}}
        <span class="pull-right">
          <router-link class="btn btn-primary" v-bind:to="'/edit/'+customer.id">
            编辑
          </router-link>
          <button class="btn btn-danger" v-on:click="deleteCustomer(customer.id)">删除</button>
        </span>
      </h1>
      <ul class="list-group">
          <li class="list-group-item">
            <span class="glyphicon glyphicon-earphone"> {{customer.phone}}</span>
          </li>
          <li class="list-group-item">
            <span class="glyphicon glyphicon-envelope"> {{customer.email}}</span>
          </li>

          <li class="list-group-item">
            <span class="glyphicon glyphicon-education"> {{customer.education}}</span>
          </li>
          <li class="list-group-item">
            <span class="glyphicon glyphicon-flag"> {{customer.graduationschool}}</span>
          </li>
          <li class="list-group-item">
            <span class="glyphicon glyphicon-plus"> {{customer.profession}}</span>
          </li>
          <li class="list-group-item">
            <span class="glyphicon glyphicon-pencil"> {{customer.profile}}</span>
          </li>
      </ul>
  </div>
</template>

<script>
export default {
  name: 'customerdetails',
  data () {
    return {
      customer: ''
    }
  },
  methods: {
    fetchCustomers (id) {
      this.$http.get('http://localhost:3000/users/' + id)
        .then(function (response) {
          // console.log(response)
          this.customer = response.body
        })
    },
    deleteCustomer (id) {
      // console.log(id)
      this.$http.delete('http://localhost:3000/users/' + id)
        .then(function (response) {
          this.$router.push({path: '/', query: {alert: '用户删除成功！'}})
        })
    }
  },
  created () {
    this.fetchCustomers(this.$route.params.id)
  }
}
</script>

<style scoped>
</style>
