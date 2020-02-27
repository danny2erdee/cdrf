<template>
  <div id="app">
   
        <el-container>
        <el-header>
          <el-menu :default-active="activeIndex2" class="el-menu-demo" mode="horizontal" @select="handleSelect"   background-color="#545c64"  text-color="#fff" active-text-color="#ffd04b">
            <el-menu-item index="1">Processing Center</el-menu-item>
            <el-submenu index="2">
              <template slot="title">Workspace</template>
              <el-menu-item index="2-1">item one</el-menu-item>
              <el-menu-item index="2-2">item two</el-menu-item>
              <el-menu-item index="2-3">item three</el-menu-item>
              <el-submenu index="2-4">
                <template slot="title">item four</template>
                <el-menu-item index="2-4-1">item one</el-menu-item>
                <el-menu-item index="2-4-2">item two</el-menu-item>
                <el-menu-item index="2-4-3">item three</el-menu-item>
              </el-submenu>
            </el-submenu>
            <el-menu-item index="3" >Info</el-menu-item>
            <el-menu-item index="4"><a href="https://www.ele.me" target="_blank">Orders</a></el-menu-item>
          </el-menu>
        </el-header>
        <el-main>
          <el-breadcrumb separator-class="el-icon-arrow-right" class="breadcrumb-container">
            <el-breadcrumb-item :to="{ path: '/hello' }">homepage</el-breadcrumb-item>
            <el-breadcrumb-item>promotion management</el-breadcrumb-item>
            <el-breadcrumb-item>promotion list</el-breadcrumb-item>
            <el-breadcrumb-item>promotion detail</el-breadcrumb-item>
          </el-breadcrumb>
          <template>
          <el-select v-model="call_format" placeholder="Songo" >
              <el-option
                v-for="item in cdr_format"
                :key="item.call_format"
                :value="item.call_format"
                :disabled="item.disabled"
               >
     
              </el-option>
            </el-select>
          <el-select v-model="call_type"  style="margin: 20px" placeholder="Select" clearable>
              <el-option
                v-for="item in cdr_options"
                :key="item.call_type"
                :value="item.call_type">
              </el-option>
            </el-select>
            <el-button type="primary" style="margin: 10px" @click="postreq()">Calculate</el-button>
          </template>

          <el-table
            :data="tableData"
            style="width: 100%; padding: 20px">
            <el-table-column
              prop="date"
              label="Date"
              width="180">
            </el-table-column>
            <el-table-column
              prop="name"
              label="Name"
              width="180">
            </el-table-column>
            <el-table-column
              prop="address"
              label="Address">
            </el-table-column>
          </el-table>
  

            <el-button-group class="button-container">
              <el-button type="primary" icon="el-icon-arrow-left">Previous Page</el-button>
              <el-button type="primary">Next Page<i class="el-icon-arrow-right el-icon-right"></i></el-button>
            </el-button-group>
        </el-main>
      </el-container>


  </div>
</template>
<script>


import axios from 'axios';

export default {
  components: {
  },
  data() {
    return {
       activeIndex2: '3',
      tableData: [{
            date: '2016-05-03',
            name: 'Tom',
            address: 'No. 189, Grove St, Los Angeles'
          }, {
            date: '2016-05-02',
            name: 'Tom',
            address: 'No. 189, Grove St, Los Angeles'
          }],
          
          cdr_options: [{
          call_type: 'Incoming'
         }, 
         {
          call_type: 'Outgoing'}],
          
          
          cdr_format: [{call_format: 'JSON'
         }, 
         {call_format: 'XML',
          disabled: true},],
      

        cdr_config: [{  
          format: '',
          type: ''
          }],
        
        call_format: '',
        call_type: '',
        cdr_url: 'http://localhost:5000/' 

    }
  },
  methods: {
 handleSelect(key, keyPath) {
        console.log(key, keyPath);
      },
  checklog: function (msg) {
      alert(msg)
    },

      postreq: function() {
     var data1 = [this.call_format, this.call_type]
            console.log(data1) 
            console.log(this.cdr_url)
            axios({ method: "POST", url: this.cdr_url, data: data1, headers: {"content-type": "text/plain" }}).then(result => {
            console.log(result.data)  
            }).catch(error => {
            console.error(error);
            });
    }
  }
}
</script>

<style>
#app {
  font-family: Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #5ea0e2;
}

.container {
  max-width: 1200px;
  margin: auto;
}

.el-header {
  background: #545c64;
}

.el-main {
  background: #EEF1F4;
}

.breadcrumb-container {
  margin-top: 20px;
  margin-bottom: 40px;
}

.el-select{
  margin-bottom: 10px;
}
.button-container {
  margin-top: 20px;
}
</style>
