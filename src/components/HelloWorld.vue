<template>
  <div>
    <div class="upload">
      <vue-csv-import
          v-model="csv"
          :fields="{customerName: {required: false, label: 'Customer Name',autoMatch:True }, orderDetails :{required: true, label: 'Order Details',autoMatch:True}, bags: {required: true, label: 'Bags',autoMatch:True}}"
      >
        <!-- <vue-csv-toggle-headers></vue-csv-toggle-headers> -->
        <vue-csv-errors></vue-csv-errors>
        <vue-csv-input></vue-csv-input>
        <vue-csv-map></vue-csv-map>
        <div>
          <label for="rowstoskip">Rows to skip</label>
          <input type="number" id="rowstoskip" name="rowstoskip" v-model="rowstoskip" placeholder="0"
          >
       </div>
      </vue-csv-import>
    </div>
    <div class="items">
      <div v-for="(item,index) in csv" class="item" v-bind:key="index" v-bind:class="{hide: index < rowstoskip}">
        <div>{{item.customerName}}</div>
        <div>{{item.orderDetails}}</div>
        <div>{{item.bags}}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data: function(){
      return {
          csv: [],
          rowstoskip: 0
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
 .upload{
     display:flex;
     flex-direction: column;
 }

 .items {
     display: table;
 }

 .items > .item {
     width: 29%;
     margin: 2%;
     display: inline-block;
 }

  .items > .item.hide{
     display:none;
 }

 h3 {
     margin: 40px 0 0;
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

 @media print {
     .upload {
         background-color: black;
         display: none;
     }
 }

</style>
