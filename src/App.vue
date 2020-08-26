<template>
  <div class="container">
    <div class="row">
      <div class="col-md-6 mx-auto">
        <h2>Https</h2>
        <div class="form-group">
          <label for="">username</label>
          <input
            type="text"
            name=""
            id=""
            class="form-control"
            placeholder=""
            aria-describedby="helpId"
            v-model="user.username"
          />
        </div>
        <div class="form-group">
          <label for="">mail</label>
          <input
            type="email"
            name=""
            id=""
            class="form-control"
            placeholder=""
            aria-describedby="helpId"
            v-model="user.email"
          />
        </div>
        <button type="submit" class="btn btn-primary" @click="submit">
          Submit
        </button>
        <hr />
        <button class="btn btn-primary" @click="fetchData">Get Data</button>
        <ul class="list-group">
          <li class="list-item" v-for="(u, index) in users" :key="index">
            {{ u.username }} - {{u.email}}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: {
        username: "",
        email: ""
      },
      users: [],
      resource:{}
    };
  },
  methods: {
    submit() {
      // this.$http
      //   .post("", this.user)
      //   .then(
      //     response => {
      //       console.log(response);
      //     },
      //     error => {
      //       console.log(error);
      //     }
      //   );
      // this.resource.save({}, this.user);
      this.resource.saveAlt(this.user)
    },
    fetchData() {
      this.$http
        .get("data.json")
        .then(response => {
          return response.json();  
        })
        .then(data => {
          const resultArray = [];
          for (let key in data) {
            resultArray.push(data[key]);
          }
          this.users = resultArray;
        });
    }
  },
  created() {
    const customsAction ={
      saveAlt: {method: 'POST', url: 'Alternative.json'}
    }
    this.resource=this.$resource('data.json', {}, customsAction);
  },
};
</script>
