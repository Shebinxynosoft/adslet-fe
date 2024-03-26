
<template>
  <!--begin::Row-->
  <div class="row g-5 g-xl-8">
    <div v-for="role in roles" :key="role.id" class="col-xl-4">
      <div class="card card-xl-stretch mb-xl-8">
        <div class="card-body">
          <h3>{{ role.name }}</h3>
        </div>
      </div>
    </div>
  </div>
  <!--end::Row-->
</template>

<script lang="ts">
import { defineComponent } from "vue";
import axios from "axios";

export default defineComponent({
  name: "widgets-lists",
  data() {
    return {
      roles: [] as any[] // Define an empty array to store roles data
    };
  },
  mounted() {
    // Fetch roles data when the component is mounted
    this.fetchRoles();
  },
  methods: {
    fetchRoles() {
      // Use axios to fetch data from the API endpoint
      axios.get("http://localhost:8000/api/roles")
        .then(response => {
          // Assign the fetched data to the roles array
          this.roles = response.data;
        })
        .catch(error => {
          console.error("Error fetching roles:", error);
          // Optionally, you can set a default error message or handle the error in another way
        });
    }
  }
});
</script>

