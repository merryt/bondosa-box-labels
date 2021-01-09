<template>
  <div>
    <div class="upload">
      <vue-csv-import
          v-model="csv"
          :fields="{rowOne: {required: false, label: 'First Slot',autoMatch:True }, rowTwo :{required: true, label: 'Second Slot',autoMatch:True}, rowThree: {required: true, label: 'Third Slot',autoMatch:True}}"
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
        <div>{{item.rowOne}}</div>
        <div>{{item.rowTwo}}</div>
        <div>{{item.rowThree}}</div>
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
 .hide{
     display:none;
 }

 .items {
     display: flex;
     flex-wrap: wrap;
 }

 .items > .item {
     width: 29%;
     margin: 2%;
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
