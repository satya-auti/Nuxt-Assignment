<template>
  <div class="sm:flex w-auto md:container sm:mx-auto md:mx-auto">
    <div
      class="md:w-2/3 sm:w-2/3 w-auto border-4 items-center border-r-0 border-gray-600 bg-gray-300"
    >
      <h1 class="bg-black text-white p-1 font-bold text-2xl text-center">
        Display User Data
      </h1>
      <input
        type="text"
        @keyup="userFindByAll(userInput)"
        v-model="userInput"
        id="userInput"
        name="userInput"
        placeholder="Search for Anything"
        class="rounded-xl ring-4 ring-stone-500 focus:ring-neutral-700 justify-center px-5 p-1 m-3"
      />
      <p class="sm:pl-1 sm:text-xs text-xs text-red-700">
        Data filtered only if it is matching with starting character...!!!
      </p>
      <hr class="sm:mt-4 sm:border-4 border-orange-600" />

      <!-- <input type="text"  @keyup="userFindByName(userName)" v-model="userName" id="userName" name="userName" placeholder="Find by Name" class="rounded-xl p-1 m-1">
            <input type="text" @keyup="userFindByEmail(userEmail)" v-model="userEmail" id="userEmail" name="userEmail" placeholder="Find by Email" class="rounded-xl p-1 m-1">
            <input type="number" @keyup="userFindByMobile(userMob)" v-model="userMob" id="userMob" name="userMob" placeholder="Find by Mob" class="rounded-xl p-1 m-1"> -->
      <!-- <input type="text" @keyup="userFindByAddress(userAddress)" v-model="userAddress" id="userName" name="userAddress" placeholder="Search for Anything" class="rounded-xl px-5 p-1 m-1"> -->
      {{ showUsers() }}
      <table
        class="sm:w-11/12 md:w-11/12 border-2 m-3 sm:text-center sm:m-3 border-stone-800"
      >
        <!-- v-show="allUserData.length>=1" -->
        <tr class="border border-1 border-stone-800">
          <th class="border border-1 border-stone-800">Name</th>
          <th class="border border-1 border-stone-800">Email</th>
          <th class="border border-1 border-stone-800">Mobile</th>
          <th class="border border-1 border-stone-800">Address</th>
          <th class="border border-1 border-stone-800" colspan="2">Action</th>
        </tr>

        <tr v-for="(user, i) in userFound" :key="user">
          <!-- <tr v-for="(user, i) in allUserData" :key="user" > -->

          <td class="border border-1 border-stone-800">{{ user.name }}</td>
          <td class="border border-1 border-stone-800">{{ user.email }}</td>
          <td class="border border-1 border-stone-800">{{ user.mobile }}</td>
          <td class="border border-1 border-stone-800">{{ user.address }}</td>
          <td class="border border-1 border-stone-800">
            <button
              @click="onEdit(i)"
              class="bg-black hover:bg-green-600 p-1 px-2 rounded-lg text-white"
              id="edit"
              type="button"
            >
              Edit
            </button>
          </td>
          <!-- v-if="deleteDisabled == true" -->
          <td class="border border-1 border-stone-800">
            <button
              @click="deleteUser(i)"
              class="bg-black hover:bg-red-600 p-1 px-2 rounded-lg text-white"
              id="delete"
              type="button"
            >
              Delete
            </button>
          </td>
        </tr>

        <!-- <tr v-for="(user, i) in userInfo" :key="user" >
                    <td class="border border-1 border-stone-800">{{user.name}}</td>
                    <td class="border border-1 border-stone-800">{{user.email}}</td>
                    <td class="border border-1 border-stone-800">{{user.mobile}}</td>
                    <td class="border border-1 border-stone-800">{{user.address}}</td>
                    <td class="border border-1 border-stone-800"><button @click="onEdit(i)" class="bg-black hover:bg-green-600 p-1 px-2 rounded-lg text-white" id="edit" type="button">Edit</button></td>
                    <td class="border border-1 border-stone-800"><button @click="deleteUser(i)" class="bg-black hover:bg-red-700 p-1 px-2 rounded-lg text-white" id="delete" type="button">Delete</button></td>
                </tr> -->
      </table>
      <!-- <div class="bg-blue-300 md:container w-1/3" > Hello div 2 -->

      <!-- </div> -->
    </div>
    <!-- <h1>Heelo2</h1> -->
    <!-- </div> -->

    <div
      class="bg-gray-300 border-4 justify-between border-l-1 border-gray-700 md:w-1/3 sm:w-1/3"
    >
      <form class="" method="post">
        <table
          class="sm:ml-12 md:ml-5 sm:w-auto w-auto md:w-auto lg:w-auto items-center sm:m-2 sm:item-center"
        >
          <caption class="w-auto">
            <h1
              id="formName"
              class="text-blue text-center md:text-left sm:text-left sm:text-3xl font-bold sm:ml-4"
            >
              Add User
            </h1>
          </caption>
          <!-- Name -->
          <tr>
            <td>
              <label for="name" class="md:text-left">Name</label>
            </td>
            <td>
              <input
                type="text"
                v-model="userData.name"
                name="name"
                id="name"
                @change="validationName"
                placeholder="Name"
                class="sm:rounded-xl placeholder:text-white bg-gray-400 sm:w-4/5 md:w-4/5 px-1 m-1 md:p-1 sm:p-1"
                required="required"
              />
            </td>
          </tr>

          <!-- Email -->
          <tr>
            <td>
              <label for="email">Email</label>
            </td>
            <td>
              <input
                type="email"
                v-model="userData.email"
                name="email"
                id="email"
                @change="validationEmail"
                placeholder="Email"
                class="sm:rounded-xl m-1 placeholder:text-white sm:w-4/5 md:w-4/5 bg-gray-400 sm:p-1"
                required="required"
              />
            </td>
          </tr>

          <!-- Mobile -->
          <tr>
            <td>
              <label for="mobile">Mobile</label>
            </td>
            <td>
              <input
                type="number"
                v-model="userData.mobile"
                name="mobile"
                id="mobile"
                @change="validationMobile"
                placeholder=" Mobile No."
                class="sm:rounded-xl bg-gray-400 m-1 sm:w-4/5 placeholder:text-white sm:p-1"
                required="required"
              />
            </td>
          </tr>

          <!-- Address -->
          <tr>
            <td>
              <label for="address">Address</label>
            </td>
            <td>
              <textarea
                name="address"
                v-model="userData.address"
                id="address"
                @change="validationAddress"
                placeholder="Address"
                class="sm:rounded-xl bg-gray-400 sm:w-4/5 md:w-4/5 placeholder:text-white m-1 sm:p-1"
                rows="3"
                required="required"
              ></textarea>
            </td>
          </tr>
          <!-- Buttons -->
          <tr>
            <td>
              <!-- ValidationNotNull -->
              <button
                @click="submitUserForm"
                class="bg-black hover:bg-blue-600 p-1 px-2 rounded-lg text-white"
                id="submit"
                type="submit"
              >
                Submit
              </button>
            </td>
            <td>
              <button
                @click="resetForm"
                class="bg-black hover:bg-red-600 p-1 px-2 rounded-lg text-white"
                id="reset"
                type="reset"
              >
                Reset
              </button>
            </td>
          </tr>
        </table>
      </form>
    </div>
  </div>
  <hr class="mt-4 border-4 border-orange-600" />
  <div>
    <hr class="sm:mt-4 border-4 border-orange-600" />
    <!-- <hr class="md:mt-4 sm:mt-4 border-4 border-orange-600"> -->

    <!-- <table  class="sm:w-auto text-center md:w-auto border-1 sm:m-3 border-stone-800"> -->
    <!-- v-show="allUserData.length>=1" -->
    <!-- <tr class="border border-1 border-stone-800">
                    <th class="border border-1 border-stone-800">Name</th>
                    <th class="border border-1 border-stone-800">Email</th>
                    <th class="border border-1 border-stone-800">Mobile</th>
                    <th class="border border-1 border-stone-800">Address</th> -->
    <!-- <th class="border border-1 border-stone-800" colspan="2">Action</th> -->

    <!-- </tr>

                <tr v-for="item in userFound" :key="item" >
                    <td class="border border-1 border-stone-800">{{item.name}}</td>
                    <td class="border border-1 border-stone-800">{{item.email}}</td>
                    <td class="border border-1 border-stone-800">{{item.mobile}}</td>
                    <td class="border border-1 border-stone-800">{{item.address}}</td> -->
    <!-- <td class="border border-1 border-stone-800"><button @click="onEdit(i)" class="bg-black hover:bg-gray-800 p-1 px-2 rounded-lg text-white" id="edit" type="button">Edit</button></td> -->
    <!-- <td class="border border-1 border-stone-800"><button @click="deleteUser(i)" class="bg-black hover:bg-red-800 p-1 px-2 rounded-lg text-white" id="delete" type="button">Delete</button></td> -->
    <!-- </tr>
            </table> -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      isEdit: false,
      indexEdit: -1,
      userName: "",
      userEmail: "",
      userMob: "",
      deleteDisabled: true,
      // userAddress: '',
      userInput: "",
      userFound: [],
      uniqueEmail: [],
      userInfo: [],
      address1: "",
      address2: "",
      name1: "",
      name2: "",
      email1: "",
      email2: "",
      mobile1: "",
      mobile2: "",
      nameMatch: "/^[A-Za-z\s]+$/",
      emailMatch: "/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/",
      // index: index + 1,
      allUserData: [],
      // i : 0,
      // show : false,
      userData: {
        name: "",
        email: "",
        mobile: "",
        address: "",
      },
    };
  },
  methods: {
    showUsers() {
      // this.allUserData = JSON.parse(sessionStorage.getItem('selectedUser')); // To get
      // this.allUserData = JSON.parse(localStorage.getItem('selectedUser')); // To get

      if (this.userInput == "") {
        this.userFound = this.allUserData;
      }
    },
    submitUserForm(event) {
      event.preventDefault(event);
      console.log(this.userData);
      //    this.validationNotNull();
      if (
        this.userData.name == "" ||
        this.userData.email == "" ||
        this.userData.mobile == "" ||
        this.userData.address == ""
      ) {
        alert("Please Enter Data Correctly");
        return;
        //         // console.log("Please Enter Address");
        // this.resetForm();
      } else {
        //         // alert("Address is valid");
        // submitUserForm();
      }

      //  //  // Validation for Name
      if (
        !isNaN(this.userData.name) ||
        this.userData.name == null ||
        this.userData.name == ""
      ) {
        alert("Please Enter Name");
        //         // console.log("Please Enter Name");
        // this.resetForm();
      } else {
        //     console.log(this.userData.name);
        //         // alert("Name is valid");
      }

      // // Validation for Mobile
      // // If x is Not a Number or less than 10 digit or greater than 9999999999
      if (
        isNaN(this.userData.mobile) ||
        this.userData.mobile < 1000000000 ||
        this.userData.mobile > 9999999999 ||
        this.userData.mobile == null ||
        this.userData.mobile == ""
      ) {
        alert("Please enter valid Mobile Number.");
        // this.resetForm();
      } else {
        //     // alert("Mobile Number is valid");
      }

      // //   // Validation for Address
      if (this.userData.address == null || this.userData.address == "") {
        alert("Please Enter Address");
        // this.resetForm();
      } else {
        //         // alert("Address is valid");
      }

      // All Check
      // if(this.userData.name=='' || this.userData.email=="" ||this.userData.mobile=='' || this.userData.address==""){
      //         alert("Please Enter Data Correctly");
      // //         // console.log("Please Enter Address");
      //         this.resetForm();
      // }else{
      // //         // alert("Address is valid");

      // }

      // Check Email id is unique or not
      this.uniqueEmail = this.allUserData.filter((e) => {
        if (e.email != this.userData.email) {
          console.log(e);
        } else {
          if (this.isEdit === true) {
            this.allUserData[this.indexEdit] = this.userData;
          } else {
            alert("Email Already Registered");
            this.resetForm();
          }
        }
      });

      if (this.isEdit === true) {
        this.deleteDisabled = false;
        this.allUserData[this.indexEdit] = this.userData;
        this.isEdit = false;
        this.indexEdit = -1;
      } else {
        // alert("unable to update");
        if (this.userData.email == "") {
          alert("Please enter unique Email Id");
        } else {
          this.allUserData.push(this.userData);
          // sessionStorage.setItem('selectedUser', JSON.stringify(this.allUserData)); // To Set
          // localStorage.setItem('selectedUser', JSON.stringify(this.allUserData)); // To Set
        }
      }

      this.userData = { name: "", email: "", mobile: "", address: "" };
      console.log(" User Form Values", this.allUserData);

      const formHead = document.getElementById("formName");
      formHead.innerText = "Add User";

      const myButton = document.getElementById("submit");
      myButton.innerText = "Submit";
    },

    //  Edit User Data
    onEdit(index) {
      console.log(this.allUserData[index]);
      // console.log(this.allUserData[this.index]);
      this.userData.name = this.allUserData[index].name;
      this.userData.email = this.allUserData[index].email;
      this.userData.mobile = this.allUserData[index].mobile;
      this.userData.address = this.allUserData[index].address;

      const formHead = document.getElementById("formName");
      formHead.innerText = "Edit User Information";

      const myButton = document.getElementById("submit");
      myButton.innerText = "Update";
      this.isEdit = true;
      this.indexEdit = index;
    },

    // Delete user from array
    deleteUser(index) {
      console.log(index);
      if (this.isEdit == true) {
        // this.resetForm();
        alert("@ the time of Editing your not allowed to delete");
      } else {
        this.allUserData.splice(index, 1);
        // userFound.splice(index, 1);
      }

      // this.resetForm();

      const formHead = document.getElementById("formName");
      formHead.innerText = "Add User";

      const myButton = document.getElementById("submit");
      myButton.innerText = "Submit";
    },

    // reset form values
    resetForm() {
      console.log("reset call");

      const formHead = document.getElementById("formName");
      formHead.innerText = "Add User";

      const myButton = document.getElementById("submit");
      myButton.innerText = "Submit";
      // indexOfEdit=-1;
      this.isEdit = false;
      this.userData = { name: "", email: "", mobile: "", address: "" };
    },

    // // Find user by Name in array
    // userFindByName(userName){
    //     console.log(userName);
    //     this.userFound = this.allUserData.filter((e) => {
    //         // if(e.name == userName)
    //         if(e.name.startsWith(userName)){
    //             console.log(e);
    //             // if(e.name.startsWith(userName))
    //             return e;

    //         }
    //     });
    //     console.log(this.userFound);
    // },

    // // Find user by Email in array
    // userFindByEmail(userEmail){
    //     console.log(userEmail);
    //     this.userFound = this.allUserData.filter((e) => {
    //         // if(e.email == userEmail)
    //         if(e.email.startsWith(userEmail)){
    //             console.log(e);
    //             return e;
    //             // alert("user Found" + e.firstName+ ""+e.lastName);
    //         }
    //     });
    //     console.log(this.userFound);
    // },

    // // Find user by Mobile in array
    // userFindByMobile(userMob){
    //     console.log(userMob);
    //     this.userFound = this.allUserData.filter((e) => {
    //         if(e.mobile == userMob){
    //         // if(e.mobile.startsWith(userMob)){
    //             console.log(e);
    //             return e;
    //             // alert("user Found" + e.firstName+ ""+e.lastName);
    //         }
    //     });
    //     console.log(this.userFound);
    // },

    // Find user by Address in array
    userFindByAll(userInput) {
      console.log(userInput);
      this.userFound = this.allUserData.filter((e) => {
        // if(e.address == userInput)
        this.address1 = userInput.toLocaleLowerCase();
        console.log(this.address1);
        this.address2 = e.address.toLocaleLowerCase();

        this.name1 = userInput.toLocaleLowerCase();
        this.name2 = e.name.toLocaleLowerCase();

        this.email1 = userInput.toLocaleLowerCase();
        this.email2 = e.email.toLocaleLowerCase();

        this.mobile1 = userInput.toString();
        this.mobile2 = e.mobile.toString();

        if (
          this.address2.startsWith(this.address1) ||
          this.name2.startsWith(this.name1) ||
          this.email2.startsWith(this.email1) ||
          this.mobile2.startsWith(this.mobile1)
        ) {
          // toLocaleLowerCase
          console.log(e);
          return e;
        }
        if (userInput == "") {
          this.userFound = this.allUserData;
        }
      });
      console.log(this.userFound);
      //   this.allUserData = JSON.parse(sessionStorage.getItem('selectedUser')); // To get
      console.log(" user Info : ", this.userInfo);
    },

    //  // Validation for Name
    validationName() {
      //  // Validation for Name
      // if(this.userData.name==''){
      this.nameMatch = /^[A-Za-z\s]+$/;
      // !this.nameMatch.test(this.userData.name) ||
      if (
        !this.nameMatch.test(this.userData.name) ||
        !isNaN(this.userData.name) ||
        this.userData.name == null ||
        this.userData.name == ""
      ) {
        // if( !isNaN(this.userData.name) || this.userData.name==null || this.userData.name==""){
        alert("Please Enter Name");
        // console.log("Please Enter Name");
        this.resetForm();
      } else {
        console.log(this.userData.name);
        // alert("Name is valid");
      }
    },

    // Validation for Email
    validationEmail() {
      // if (/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(this.userData.email)){

      this.emailMatch = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
      // if(this.userData.email.matchAll(this.emailMatch)){
      if (this.emailMatch.test(this.userData.email)) {
        // alert("Email is valid");
        // console.log("Email is valid");
      } else {
        alert("Email is Invalid");
        this.resetForm();
      }
    },

    // Validation for Mobile
    validationMobile() {
      // Validation for Mobile
      // If x is Not a Number or less than 10 digit or greater than 9999999999
      if (
        isNaN(this.userData.mobile) ||
        this.userData.mobile < 1000000000 ||
        this.userData.mobile > 9999999999
      ) {
        alert("Mobile Number is Invalid");
        this.resetForm();
      } else {
        // alert("Mobile Number is valid");
      }
    },

    //   // Validation for Address
    validationAddress() {
      //   // Validation for Address
      // if(this.userData.address!=''){
      if (this.userData.address == null || this.userData.address == "") {
        // this.userData.address2.length<6
        alert("Please Enter Address");
        // console.log("Please Enter Address");
        this.resetForm();
      } else {
        // alert("Address is valid");
      }
    },

    validationNotNull() {
      if (
        this.userData.name == "" ||
        this.userData.email == "" ||
        this.userData.mobile == "" ||
        this.userData.address == ""
      ) {
        alert("Please Enter Data Correctly");
        return;
        //         // console.log("Please Enter Address");
        // this.resetForm();
      } else {
        //         // alert("Address is valid");
        // submitUserForm();
      }
    },
  },
};
</script>
