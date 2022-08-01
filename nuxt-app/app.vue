<template>

  <main class="flex justify-center w-full h-screen">
        
<link href="https://unpkg.com/tailwindcss@^1.0/dist/tailwind.min.css" rel="stylesheet">
    
    <div>
        
       
      <form
        @submit="formSubmit"
        class="bg-gray-100 border-red-500 rounded-lg border-2 px-12"
      >
        <table>
          <h2 class="text-teal-600 text-xl font-bold pt-6">User Registration</h2>
          <hr />
          <br />
          <label class="pt-10 py-10" for="name">Name:</label
          ><br />
          <input
           @keyup="userFindByName(name)"  
            type="text"
             v-model="user.name"
           
            id="name"
            name="name"
            placeholder="Enter your Name"
          /><br /><br />

          <label class="pt-10 py-10" for="email">Email:</label
          ><br />
          <input
            type="text"
            v-model="user.email"
            id="email"
            name="email"
            placeholder="Enter your Mail"
            @click="ValidateEmail(document.form1.text1)"
          /><br /><br />

          <label for="number">Mobile: </label
          ><br />
          <input
            type="number"
            v-model="user.number"
            id="number"
            name="number"
            placeholder="Enter your number"
          />
          <br /><br />

          <label for="address"> Address: </label
          ><br />
          <input
            type="text"
            v-model="user.address"
            id="address"
            name="address"
            placeholder="Enter your address"
          />
          <br /><br />

          <!-- <label for="text">City: </label
          ><br /> -->
          <!-- <input
            type="text"
            v-model="user.city"
            id="city"
            name="city"
            placeholder="Enter your city"
          />
          <br /><br /> -->
          <div>
            <!-- <button
              class="py-1 px-5 mr-5 bg-black hover:bg-blue-900 text-white text-center rounded-md mb-3"
              type="submit"
              @click="formSubmit"> Submit </button> -->

              <!-- <button v-if="onEdit()"
              class="py-1 px-5 mr-5 bg-black hover:bg-blue-900 text-white text-center rounded-md mb-3"
              type="submit"
              @click="formSubmit"> Edit User </button> -->

             
              <button 
              class="py-1 px-5 mr-5 bg-black hover:bg-blue-900 text-white text-center rounded-md mb-3"
              type="submit"
              @click="formSubmit"> Submit</button>

            


          
            <button
              class="py-1 px-5 bg-black hover:bg-blue-900 text-white text-center rounded-md mb-3"
              type="reset"
            >
              Reset
            </button>
            
          </div>
        </table>
      </form>
      <br />
        <input type="text" id="myInput" onkeyup="myFunction()" placeholder="Search for names..">
       
      
      <br />


      
      <table class="list" id="myTable">
        <tr >
          <!-- <th class="px-4 border-black rounded-lg border-2">id</th> -->
          <th class="px-4 border-blue-400 rounded-lg border-2">Name</th>
           <th class="px-4 border-blue-400 rounded-lg border-2">Email</th>
                   <th class="px-4 border-blue-400 rounded-lg border-2">Mobile</th>

          <th class="px-4 border-blue-400 rounded-lg border-2">Address</th>
          
 
          <th class="px-4 border-blue-400 rounded-lg border-2">Action</th>
        </tr>
        <tr v-for="(item, index) in users" v-bind:index="index" :key="item" id="names"  class="header">
          <!-- <td class="px-4 border-black rounded-lg border-2">{{item.id=i+1}}</td> -->
          <td class="px-4 border-blue-400 rounded-lg border-2">
            {{ item.name }}
          </td>

          <td class="px-4 border-blue-400 rounded-lg border-2">
            {{ item.email }}
          </td>
          <td class="px-4 border-blue-400 rounded-lg border-2">
            {{ item.number }}
          </td>
          <td class="px-4 border-blue-400 rounded-lg border-2">
            {{ item.address }}
          </td>
          <td class="px-4 border-blue-400 rounded-lg border-2">
            {{ item.Action }}
            <button
              class="mx-3 rounded-lg bg-red-400 hover:bg-red-600 text-white w-20"
              @click="userDelete(index)"
            >
              Delete
            </button>
            <button
              class="mx-3 rounded-lg bg-green-400 hover:bg-green-600 text-white w-20"
              @click="onEdit(index)"
            >
              Edit
            </button>
          </td>
        </tr>
      </table>
 
      <br />
      <!-- <h3>Search by name</h3>
      <form >
         <input type="text" placeholder="Search.." name="search" style=" width: 80%;">
         <button type="submit"><i class="fa fa-search"></i>Search here</button>
  
         
      </form> -->
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      isEdit: false,
      indexEdit: -1,
      users: [],
      userName: '',
     
      allUserData : [],
      user: {
        name: "",
        email:"",
         number: "",
         

        address: "",
      
       
      },
    };
  },
  methods: {
    formSubmit(event) {
      event.preventDefault();
      if (this.isEdit == true) {
        this.users[this.indexEdit] = this.user;
        this.isEdit = false;
        this.indexEdit = -1;
      } else {
        this.users.push(this.user);
      }
      this.user = {
        name: "",
       email:"",
        number: "",
     address: "",
    
       
      }
      
    },
   
myFunction() {
      // Declare variables
      var input, filter, table, tr, td, i, txtValue;
      input = document.getElementById("myInput");
      filter = input.value.toUpperCase();
      table = document.getElementById("myTable");
      tr = table.getElementsByTagName("tr");
    
      // Loop through all table rows, and hide those who don't match the search query
      for (i = 0; i < tr.length; i++) {
        td = tr[i].getElementsByTagName("td")[0];
        if (td) {
          txtValue = td.textContent || td.innerText;
          if (txtValue.toUpperCase().indexOf(filter) > -1) {
            tr[i].style.display = "";
          } else {
            tr[i].style.display = "none";
          }
        }
      }
    },
  

  

    onReset(event) {
      event.preventDefault();
     
      this.form.name = "";
       this.form.email = "";
         this.form.contact = "";
      this.form.address = "";
    
     
    },
    userDelete(index) {
      this.users.splice(index, 1);
    },
    onEdit(index) {
      this.user.name = this.users[index].name;
       this.user.email = this.users[index].email;
        this.user.number = this.users[index].number;

      this.user.address = this.users[index].address;
      //this.user.city = this.users[index].city;
     
      this.isEdit = true;
      this.indexEdit = index;
      //this.user.action=action;
    },
    
  },
};
</script>


    <style>
        #myInput {
  background-image: url('/css/searchicon.png'); /* Add a search icon to input */
  background-position: 10px 12px; /* Position the search icon */
  background-repeat: no-repeat; /* Do not repeat the icon image */
  width: 100%; /* Full-width */
  font-size: 16px; /* Increase font-size */
  padding: 12px 20px 12px 40px; /* Add some padding */
  border: 1px solid #ddd; /* Add a grey border */
  margin-bottom: 12px; /* Add some space below the input */
}

#myTable {
  border-collapse: collapse; /* Collapse borders */
  width: 100%; /* Full-width */
  border: 1px solid #ddd; /* Add a grey border */
  font-size: 18px; /* Increase font-size */
}

#myTable th, #myTable td {
  text-align: left; /* Left-align text */
  padding: 12px; /* Add padding */
}

#myTable tr {
  /* Add a bottom border to all table rows */
  border-bottom: 1px solid #ddd;
}

#myTable tr.header, #myTable tr:hover {
  /* Add a grey background color to the table header and on hover */
  background-color: #f1f1f1;
}

    </style>


