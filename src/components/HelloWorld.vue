<template>
  <div>
    <div class="upload">
      <vue-csv-import
          v-model="csv"
          :fields="{rowOne: {required: false, label: 'First Slot'}, rowTwo :{required: true, label: 'Second Slot'}, rowThree: {required: true, label: 'Third Slot'}}"
      >
        <vue-csv-toggle-headers></vue-csv-toggle-headers>
        <vue-csv-errors></vue-csv-errors>
        <vue-csv-input></vue-csv-input>
        <vue-csv-map></vue-csv-map>
      </vue-csv-import>
    </div>
    <div class="items">
      <div v-for="item in csv" class="item" v-bind:key="item.rowOne">
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
          csv: "Please upload a CSV"
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
     display: flex;
     flex-wrap: wrap;
 }

 .items > .item {
     width: 44%;
     margin: 3%;
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
