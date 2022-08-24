<template>
  <div class="w-1/6 m-auto pt-5">
    <Accordion title="Add New Location      +">
      <form>
        <div class="form-group">
          <span for="title" class="pull-left">Title*</span>
          <div>
            <input
              type="text"
              placeholder="Enter Title"
              v-model="offices.title"
              class="
                text-sm text-gray-base
                w-full
                mr-1
                py-3
                px-2
                h-1
                border border-gray-10
                rounded
                mb-1
              "
            />
          </div>
        </div>
        <br />
        <div class="form-group">
          <span for="address" class="pull-left">Enter the address*</span>
          <input
            type="text"
            id="address"
            placeholder="Enter Address"
            v-model="offices.address"
            class="
              text-sm text-gray-base
              w-full
              mr-1
              py-3
              px-2
              h-1
              border border-gray-10
              rounded
              mb-1
            "
          />
        </div>
        <br />
        <span style="color: #34a6b9" class="pull-left">Contact information</span
        ><br />
        <br />
        <hr style="1px solid lightgray" />

        <div class="form-group">
          <span for="fullname" class="pull-left">Full Name*</span>
          <input
            type="text"
            id="fullname"
            placeholder="Enter Full Name"
            v-model="offices.fullname"
            class="
              text-sm text-gray-base
              w-full
              mr-1
              py-3
              px-2
              h-1
              border border-gray-10
              rounded
              mb-1
            "
          />
        </div>
        <br />
        <div class="form-group">
          <span for="jobposition" class="pull-left">Job Position*</span>
          <input
            type="text"
            id="jobposition"
            placeholder="Enter Job Position"
            v-model="offices.job"
            class="
              text-sm text-gray-base
              w-full
              mr-1
              py-3
              px-2
              h-1
              border border-gray-10
              rounded
              mb-1
            "
          />
        </div>
        <br />
        <div class="form-group">
          <span for="email" class="pull-left">Email address*</span>
          <input
            type="email"
            id="email"
            placeholder="name@example.com"
            v-model="offices.email"
            class="
              text-sm text-gray-base
              w-full
              mr-1
              py-3
              px-2
              h-1
              border border-gray-10
              rounded
              mb-1
            "
          />
        </div>
        <br />
        <div class="form-group">
          <span for="phone" class="pull-left">Phone*</span>
          <input
            type="phone"
            id="phone"
            v-model="offices.phone"
            placeholder="(xxx)xxx-xxxx"
            class="
              text-sm text-gray-base
              w-full
              mr-1
              py-3
              px-2
              h-1
              border border-gray-10
              rounded
              mb-1
            "
            required
          />
        </div>
        <br />
        <button
          type="button"
          v-on:click="add"
          class="
            bg-blue-500
            hover:bg-blue-700
            text-white
            font-bold
            py-2
            px-4
            rounded
          "
        >
          Save
        </button>
      </form>
    </Accordion>
    <div
      style="bg-color: #34a6b9"
      v-for="item in offices"
      :key="item.id"
      class="w-1/2 m-auto pt-4"
    >
      <table border="1">
        <tr>
          <Accordion title="Headqueter">
            <td>{{ item.title }}</td>
            <br />
            <td>{{ item.address }}</td>
            <br />
            <td>{{ item.fullname }}</td>
            <br />
            <td>{{ item.job }}</td>
            <br />
            <td>{{ item.email }}</td>
            <br />
            <td>{{ item.phone }}</td>
            <br />
            <td>
              <hr />
              <router-link
                :to="'/add/' + item.id"
                class="
                  bg-blue-500
                  hover:bg-blue-400
                  text-white
                  font-bold
                  py-3
                  px-5
                  border-b-4 border-blue-700
                  hover:border-blue-500
                  rounded
                "
                >Edit</router-link
              >
            </td>
            <td>
              <button
                v-on:click="del(item.id)"
                class="
                  bg-blue-500
                  hover:bg-red-400
                  text-white
                  font-bold
                  py-3
                  px-3
                  border-b-4 border-blue-700
                  hover:border-blue-500
                  rounded
                "
              >
                Delete
              </button>
            </td>
          </Accordion>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
import Accordion from "../components/Accordion.vue";
import axios from "axios";
export default {
  name: "App",
  components: {
    Accordion,
  },
  data() {
    return {
      name: "",
      offices: [],
      offices: {
        title: "",
        address: "",
        jon: "",
      },
    };
  },
  methods: {
    async del(id) {
      let result = await axios.delete("http://localhost:3000/offices/" + id);
      if ((result.status = 200)) {
        this.loaddata();
      }
    },
    async loaddata() {
      let result = await axios.get("http://localhost:3000/offices");
      console.warn(result);
      this.offices = result.data;
    },
    async add() {
      console.warn(this.offices);
      const result = await axios.post("http://localhost:3000/offices", {
        title: this.offices.title,
        address: this.offices.address,
        fullname: this.offices.fullname,
        job: this.offices.job,
        email: this.offices.email,
        phone: this.offices.phone,
      });
      if (result.status == 201) {
        this.$router.push({ name: "index" });
        this.loaddata();
      }
      console.warn("result", result);
    },
  },
  mounted() {
    this.loaddata();
  },
};
</script>

