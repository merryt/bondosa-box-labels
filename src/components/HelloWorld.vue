<template>
  <div>
    <div class="upload">
      <vue-csv-import
        v-model="csv"
        :fields="{
          customerName: {
            required: false,
            label: 'Customer Name',
            autoMatch: True
          },
          dietaryRestrictions: {
            required: true,
            label: 'Dietary Restrictions',
            autoMatch: True
          },
          orderDetails: {
            required: true,
            label: 'Order Details',
            autoMatch: True
          },
          bags: { required: true, label: 'Bags', autoMatch: True },
          driver: { required: false, label: 'Driver', autoMatch: True },
          stopNumber: { required: false, label: 'Stop Number', autoMatch: True }
        }"
      >
        <!-- <vue-csv-toggle-headers></vue-csv-toggle-headers> -->
        <vue-csv-errors></vue-csv-errors>
        <vue-csv-input></vue-csv-input>
        <vue-csv-map :noThead="true"></vue-csv-map>
        <div>
          <!-- <label for="rowstoskip">Rows to skip</label>
               <input type="number" id="rowstoskip" name="rowstoskip" v-model="rowstoskip" placeholder="0"
               > -->
        </div>
      </vue-csv-import>
      <hr />
      <ul>
        <!-- <li>Header rows will automatically be skipped.</li> -->
        <li>
          If there isn't a quantity of bags or a name it won't get published
        </li>
      </ul>
    </div>
    <div class="items">
      <template v-for="(item, index) in csv" v-bind:key="index">
        <template v-if="parseInt(item.bags)">
          <div
            v-for="bag in parseInt(item.bags)"
            class="item"
            v-bind:key="bag"
            v-bind:class="{ hide: index < rowstoskip || !item.customerName }"
          >
            <div>
              <strong>{{ item.customerName }}</strong>
            </div>
            <div v-if="item.dietaryRestrictions">
              <em>{{ item.dietaryRestrictions }}</em>
            </div>
            <div>
              <em>{{ item.orderDetails }}</em>
            </div>
            <div>
              bag <strong>{{ bag }}</strong> of <strong>{{ item.bags }}</strong>
            </div>
            <div v-if="item.driver" class="driver">
              <p>Driver #: {{ item.driver }}</p>
              <p>Stop #:{{ item.stopNumber }}</p>
            </div>
          </div>
        </template>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data: function() {
    return {
      csv: [],
      rowstoskip: 0
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.upload {
  display: flex;
  flex-direction: column;
}
.upload > input {
  margin: 0 auto 20px auto;
}

.items {
  display: table;
}

.items > .item {
  width: 29%;
  margin: 2%;
  display: inline-block;
}

.items > .item.hide {
  display: none;
}
.driver {
  display: flex;
  justify-content: space-around;
}

h3 {
  margin: 40px 0 0;
}
li {
  text-align: left;
}
a {
  color: #42b983;
}

@media print {
  .upload {
    background-color: black;
    display: none;
  }
}
</style>
