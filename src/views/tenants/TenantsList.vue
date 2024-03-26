<template>
    <!--begin::Tables Widget 9-->
    <div class="card" :class="widgetClasses">
      <!--begin::Header-->
      <div class="card-header border-0 pt-5">
        <h3 class="card-title align-items-start flex-column">
          <span class="card-label fw-bold fs-3 mb-1">Tenants List</span>
        </h3>
  
        <div
          class="card-toolbar"
          data-bs-toggle="tooltip"
          data-bs-placement="top"
          data-bs-trigger="hover"
          title="Click to add a user"
        >
          <a
            href="#"
            class="btn btn-sm btn-light-primary"
            data-bs-toggle="modal"
            data-bs-target="#exampleModal"
          >
            <KTIcon icon-name="plus" icon-class="fs-3" />
            New Tenants
          </a>
        </div>
      </div>
      <!--end::Header-->
  
      <!-- Modal -->
      <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true" ref="modal">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h1 class="modal-title fs-5" id="exampleModalLabel">Create Tenants</h1>
              <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
              <div class="mb-6">
                <label for="name" class="form-label">Name</label>
                <input type="text" name="name" class="form-control" id="name" placeholder="Enter Name">
              </div>
              <div class="mb-3">
                <label for="slug" class="form-label">Slug</label>
                <input type="text" class="form-control" id="slug" name="slug" placeholder="Slug name">
              </div>
              <div class="mb-3">
                <label for="email" class="form-label">Email address</label>
                <input type="email" class="form-control" id="email" name="email" placeholder="name@example.com">
              </div>
              <div class="mb-6">
                <label for="no_of_terminals" class="form-label">No of Terminals</label>
                <input type="text" class="form-control" id="no_of_terminals" name="no_of_terminals" placeholder="No of Terminals">
              </div>
              <div class="mb-3">
                <label for="phone_number" class="form-label">Phone Number</label>
                <input type="text" class="form-control" id="phone_number" name="phone_number" placeholder="Phone Number">
              </div>
              <div class="mb-3">
                <label for="wallet" class="form-label"> Wallet</label>
                <input type="text" class="form-control" id="wallet" name="wallet" placeholder="Wallet">
              </div>
              <div class="mb-3">
                <label for="Address" class="form-label">Address</label>
                <textarea class="form-control" id="address" name="address" rows="3"></textarea>
              </div>
            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
              <button type="submit" class="btn btn-primary" @click.prevent="saveTenant">Save</button>
            </div>
          </div>
        </div>
      </div>
      <!-- Modal -->
  
      <!--begin::Body-->
      <div class="card-body py-3">
        <!--begin::Table container-->
        <div class="table-responsive">
          <!--begin::Table-->
          <table class="table table-row-dashed table-row-gray-300 align-middle gs-0 gy-4">
            <!--begin::Table head-->
            <thead>
              <tr class="fw-bold text-muted">
                <th>Name</th>
                <th>Slug</th>
                <th>Email</th>
                <th>No of Terminals</th>
                <th>Phone Number</th>
                <th>Wallet</th>
                <th>Actions</th>
              </tr>
            </thead>
            <!--end::Table head-->
  
            <!--begin::Table body-->
            <tbody>
              <tr v-for="tenant in tenants" :key="tenant.id">
                <td>{{ tenant.name }}</td>
                <td>{{ tenant.slug }}</td>
                <td>{{ tenant.email }}</td>
                <td>{{ tenant.no_of_terminals }}</td>
                <td>{{ tenant.phone_number }}</td>
                <td>{{ tenant.wallet }}</td>
                <td>
                    <a href="#" class="btn btn-icon btn-bg-light btn-active-color-primary btn-sm me-1">
                    <KTIcon icon-name="switch" icon-class="fs-3" />
                    </a>

                    <a href="#" class="btn btn-icon btn-bg-light btn-active-color-primary btn-sm me-1" @click="editTenant(tenant.id)">
                    <KTIcon icon-name="pencil" icon-class="fs-3" />
                    </a>

                    <a href="#" class="btn btn-icon btn-bg-light btn-active-color-primary btn-sm">
                    <KTIcon icon-name="trash" icon-class="fs-3" />
                    </a>
                </td>
              </tr>
            </tbody>
            <!--end::Table body-->
          </table>
          <!--end::Table-->
        </div>
        <!--end::Table container-->
      </div>
      <!--begin::Body-->
    </div>
    <!--end::Tables Widget 9-->
  </template>

<script lang="ts">
import { defineComponent, ref, onMounted } from "vue";
import axios from 'axios';

export default defineComponent({
  name: "TenantsComponent",
  props: {
    widgetClasses: String,
  },
  setup() {
 interface Tenant {
  id: number;
  name: string;
  slug: string;
  email: string;
  no_of_terminals: string;
  phone_number: string;
  wallet: string;
}
const tenants = ref<Tenant[]>([]); 

    onMounted(async () => {
      try {
        const response = await axios.get('http://localhost:8000/api/tenants');
        tenants.value = response.data.data; // Assuming data is nested under 'data' key
      } catch (error) {
        console.error('Error fetching tenants:', error);
      }
    });

    return {
      tenants,
    };
  },
  methods: {
    // Move the saveTenant function here
    saveTenant() {
      // Retrieve form data
      const formData = {
      name: (document.getElementById('name') as HTMLInputElement)?.value ?? '',
      slug: (document.getElementById('slug') as HTMLInputElement)?.value ?? '',
      email: (document.getElementById('email') as HTMLInputElement)?.value ?? '',
      no_of_terminals: (document.getElementById('no_of_terminals') as HTMLInputElement)?.value ?? '',
      phone_number: (document.getElementById('phone_number') as HTMLInputElement)?.value ?? '',
      wallet: (document.getElementById('wallet') as HTMLInputElement)?.value ?? '',
      address: (document.getElementById('address') as HTMLTextAreaElement)?.value ?? ''
      };
     

      // Send POST request to your backend API
     axios.post('http://localhost:8000/api/tenants', formData)
      .then(function (response) {
        // Handle success
        console.log(response);
        alert('Tenant saved successfully!');
        // Hide the modal
        this.$refs.modal.hide();
      }.bind(this))
      .catch(function (error) {
        // Handle error
        console.error(error);
        alert('Failed to save tenant. Please try again.');
      }.bind(this));
    }
  }
});
</script>