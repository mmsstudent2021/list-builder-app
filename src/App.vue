<template>
  <div class="border m-3 p-3">
    <h1 v-bind:class="{'text-primary':h1ColorStatus}">{{ title }}</h1>
    <ul class="list-group">
      <li class="list-group-item d-flex justify-content-between" v-for="(list,index) in lists" v-bind:key="index">
        <div class="form-check">
          <input
              class="form-check-input"
              type="checkbox" value=""
              v-bind:id="`check`+list.id"
              v-bind:checked="list.isFinish"
              v-on:change="list.isFinish = !list.isFinish"
          >
          <label class="form-check-label" v-bind:for="`check`+list.id">
            <span v-bind:class="{'text-decoration-line-through':list.isFinish}">{{ list.job }}</span>
          </label>
        </div>
        <button class="btn btn-sm btn-outline-danger" v-on:click="del(list.id)">
          <i class="bi bi-trash"></i>
        </button>

      </li>
    </ul>
    <form class="row mt-2 g-2" action="" v-on:submit.prevent="addList">
      <div class="col-8">
        <input  class="form-control" type="text" v-model="input" required>
      </div>
      <div class="col-4">
        <button class="btn btn-primary w-100">Add</button>
      </div>
    </form>

<!--    <img v-if="lightStatus" v-bind:src="lightOn" alt="">-->
<!--    <img v-else v-bind:src="lightOff" alt="">-->

<!--    <button v-on:click="lightStatus=true">On</button>-->
<!--    <button v-on:click="lightStatus=false">Off</button>-->

<!--    <button-->
<!--        v-on:click="lightStatus = !lightStatus"-->
<!--        class="btn btn-outline-primary"-->
<!--        v-bind:class="{'active':lightStatus}"-->
<!--    >-->
<!--      Switch-->
<!--    </button>-->

  </div>
</template>

<script>
import Swal from 'sweetalert2'
export default {
  data() {
    return {
      title : "List Builder",
      lists : [
        {
          id:1,
          job:"To Sleep",
          isFinish:true
        },
        {
          id:2,
          job:"To Eat",
          isFinish:false
        },
        {
          id:3,
          job:"To Read Books",
          isFinish:true
        },
        {
          id:4,
          job:"To attend MMS IT",
          isFinish:false
        },
      ],
      input:null,
      h1ColorStatus : true,
      lightOn : "https://www.w3schools.com/js/pic_bulbon.gif",
      lightOff : "https://www.w3schools.com/js/pic_bulboff.gif",
      lightSrc : "https://www.w3schools.com/js/pic_bulboff.gif",
      lightStatus : false,

    }
  },
  methods: {
    addList() {
      // this.lists.push(this.input);
      // this.input = null
      let newList = {
        id : this.lists[this.lists.length-1].id + 1,
        job : this.input,
        isFinish : false
      }

      // this.lists.push(newList)
      this.lists = [...this.lists,newList]
      this.input = null
    },
    del(id){
      console.log(id);
      Swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        icon: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, delete it!'
      }).then((result) => {
        if (result.isConfirmed) {
          this.lists = this.lists.filter(list => list.id !== id )
          const Toast = Swal.mixin({
            toast: true,
            position: 'top-end',
            showConfirmButton: false,
            timer: 3000,
            timerProgressBar: true,
            didOpen: (toast) => {
              toast.addEventListener('mouseenter', Swal.stopTimer)
              toast.addEventListener('mouseleave', Swal.resumeTimer)
            }
          })

          Toast.fire({
            icon: 'success',
            title: 'Signed in successfully'
          })
        }
      })
      // this.lists.splice(index,1);
    }
  },
}
</script>

<style>

@import "bootstrap-icons/font/bootstrap-icons.css";
@import "bootstrap/dist/css/bootstrap.min.css";

</style>