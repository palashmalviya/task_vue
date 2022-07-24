<template>
  <div class="container">
    <!-- <table id="info_table">
      <thead>
        <tr class="thead-dark">
          <th>Id</th>
          <th>Brewery Id</th>
          <th>Name</th>
          <th>Category Id</th>
          <th>Style Id</th>
          <th>ADV</th>
          <th>IBU</th>
          <th>SRM</th>
          <th>UPC</th>
          <th>Added By</th>
          <th>Last Updated</th>
          <th>Description</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="d in data" >
          <td>{{d.id}}</td>
          <td>{{d.brewery_id}}</td>
          <td>{{d.name}}</td>
          <td >{{d.cat_id}}</td>
          <td>{{d.style_id}}</td>
          <td>{{d.abv}}</td>
          <td>{{d.ibu}}</td>
          <td>{{d.srm}}</td>
          <td>{{d.upc}}</td>
          <td>{{d.add_user}}</td>
          <td>{{d.last_mod}}</td>
          <td>$</td>

        </tr>
      </tbody>
    </table> -->
   

      <table id="info_table">
        <thead>
          <tr>
            <th  v-for="(col,i) in columns" :key="i" v-on:click="sortTable(col)"> <p :id="'col' + i" >{{col}}</p></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(row,i) in get_rows()" :key="i" :id="'row' + i">
            <td v-for="(col,i) in columns" > <p :id="'dcol' + i" :title=row[col]>{{row[col]}}</p> </td>
          </tr>
        </tbody>
      </table>
  </div>
  <div>
        <span class="pgbtn"
          v-for="i in num_pages()"
          v-bind:class="[i == currentPage ? 'active' : '']"
          v-on:click="change_page(i)">{{i}}</span>
      </div>

<br>
<br>
<br>
<h1 style="text-align:center"> ------------------------- IN CARD -----------------------</h1>

  <div class="container_">
  <div class="card" v-for="d in data">
    <div class="box">
      <div class="content">
        <h2>{{d.id}}</h2>
        <h3>{{d.brewery_id}} <br> {{d.name}}</h3>
        <p>Style Id : {{d.style_id}}</p>
        <p>Category Id : {{d.cat_id}}</p>
        <p>Last Modified Id : {{d.last_mod}}</p>
      </div>
    </div>
  </div>
</div>
</template>

<script>
  export default{
    data(){
      return{
        data:[],
        ascending: false,
        sortColumn: '',
        currentPage: 1,
        elementsPerPage: 9,
      }
    },
    mounted(){
      fetch("http://localhost:3000/data")
      .then((res) => res.json())
      .then(data => this.data = data)
      .catch(err=> console.log(err.message))
    },

    methods :{
       
      "sortTable": function sortTable(col) {
        if (this.sortColumn === col) {
          this.ascending = !this.ascending;
        } else {
          this.ascending = true;
          this.sortColumn = col;
        }

        var ascending = this.ascending;

        this.data.sort(function(a, b) {
          if (a[col] > b[col]) {
            return ascending ? 1 : -1
          } else if (a[col] < b[col]) {
            return ascending ? -1 : 1
          }
          return 0;
        }) 
      },
        "num_pages": function num_pages() {
          return Math.ceil(this.data.length / this.elementsPerPage);
        },
        "get_rows": function get_rows() {
          var start = (this.currentPage-1) * this.elementsPerPage;
          var end = start + this.elementsPerPage;
          return this.data.slice(start, end);
        },
        "change_page": function change_page(page) {
          this.currentPage = page;
        }

    },
    
    computed:{
      "columns": function columns() {
        if (this.data.length == 0) {
          return [];
        }
        return Object.keys(this.data[0])
      },
      

             
    }
  }
</script>


<style>
.container {
  display: grid;
  justify-content: center;
  align-items: center;
  overflow-x:auto;
}

table {
  border-collapse: collapse;
  box-shadow: 0px 10px 20px 2px gray;
  background-color: white;
  text-align: left;
  overflow: hidden;
  text-align: center;
  margin-bottom: 50px;
  margin-top: 10px;
  width: 100%; 
}

thead {
    box-shadow: 12px 5px 10px rgba(153, 122, 122, 0.671);
  }

  th {
    padding: 18px 20px;
    text-transform: uppercase;
    font-size: 16px;
    font-weight: 1200;
    cursor: pointer;
    background-color: rgb(22, 38, 68);
    color: white;
  }

  td {
    padding: 8px 18px;
    width: auto;
    white-space: nowrap;
  }
  tr{
    
    box-shadow: 3px 3px 3px rgba(72, 77, 122, 0.637);
  }

  tr:nth-child(even) {
    background-color: rgba(231, 227, 219, 0.377);
  }

  #col9, #dcol9,#col11, #dcol11{
    display : none;
  }

  #col10, #dcol10{
    width: 120px;
    
  overflow: hidden;
  text-overflow: ellipsis; 
  }

  .pgbtn {
  width: 10%;
  margin: 2px;
  padding : 10px 10px;
  border-color: rgb(106, 106, 187);
  color: #fff;
  box-shadow: 0 0 40px 40px rgb(73, 73, 114) inset, 0 0 0 0  rgb(46, 46, 78);
  transition: all 150ms ease-in-out;
  }

  .pgbtn:hover {
    cursor: pointer;
    color: black;
    box-shadow: 0 0 6px 0  rgb(34, 34, 68) inset, 0 0 10px 4px  rgb(47, 47, 87);
  }


.container_ {
  justify-content: center;
  align-items: center;
  overflow-x:auto;
  width: 100%; 
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  min-width: 800px;
  margin: 20px 0;
  margin-bottom: 80px;
}

.container_ .card {
  position: relative;
  min-width: 350px;
  height: 420px;
  box-shadow: inset 0px 0px 50px rgba(0, 0, 0, 0.274);
  border-radius: 15px;
  margin: 20px;
  transition: 0.5s;
  
}



.container_ .card .box {
  position: absolute;
  top: 20px;
  left: 0px;
  right: 0px;
  bottom: 20px;
  background: linear-gradient(to right, #0f0c29, #191631, #24243e);
  border-radius: 15px;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
  transition: 0.5s;
  
}

.container_ .card .box:hover {
  transform: translateY(-20px);
  height: 420px;
  background: linear-gradient(to right, #24243e, #191631, #0f0c29);
}



.container_ .card .box .content {
  padding: 20px;
  text-align: center;
   overflow: auto;

}

.container_ .card .box .content h2 {
  position: absolute;
  top: -140px;
  right: 30px;
  font-size: 8rem;
  color: rgba(255, 255, 255, 0.089);
}

.container_ .card .box .content h3 {
  font-size: 1.8rem;
  color: #fff;
  z-index: 1;
  transition: 0.5s;
  margin-bottom: 15px;
}

.container_ .card .box .content p {
  font-size: 1rem;
  font-weight: 200;
  color: rgba(255, 255, 255, 0.9);
  z-index: 1;
  transition: 0.5s;
   
}

.container_ .card .box .content a:hover {
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.6);
  background-image: linear-gradient(to right, #4ca1af, #2c3e50);
  color: #000;
  font-weight: 900;
}

</style>
