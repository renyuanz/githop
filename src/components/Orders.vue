<template>
  <div class="hello">
    <p v-for="(order, i) in orders.edges" :key="i">
      {{ order.cursor }}
    </p>
  </div>
</template>

<script>
import gql from 'graphql-tag';

export default {
  name: 'Orders',
  data() {
    return {
      orders: {},
    };
  },
  apollo: {
    // Query with parameters
    orders: {
      // gql query
      query: gql`query orders($last: Int) {
        orders(last: $last) {
          edges {
            cursor
            node {
              id
              name
            }
          }
        }
      }`,
      // Static parameters
      variables: {
        last: 3,
      },
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
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
  color: #42b983;
}
</style>
