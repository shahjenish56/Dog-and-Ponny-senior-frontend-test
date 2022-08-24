

<template>
  <div class="w-1/6 m-auto pt-5 border-2 p-0 rounded mt-0">
    <form style="border-1">
      <div class="form-group border-1">
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
          v-model="job"
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
        Update
      </button>
    </form>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "add",
  data() {
    return {
      offices: {
        title: "",
        address: "",
      },
    };
  },
  methods: {
    async add() {
      console.warn(this.offices);
      const result = await axios.put(
        "http://localhost:3000/offices/" + this.$route.params.id,
        {
          title: this.offices.title,
          address: this.offices.address,
          fullname: this.offices.fullname,
          job: this.offices.job,
          email: this.offices.email,
          phone: this.offices.phone,
        }
      );
      if (result.status == 200) {
        this.$router.push({ name: "index" });
      }
      console.warn("result", result);
    },
  },
  async mounted() {
    const result = await axios.get(
      "http://localhost:3000/offices/" + this.$route.params.id
    );
    console.warn(result.data);
    //console.warn(this.$route.params.id);
    this.offices = result.data;
  },
};
</script>


