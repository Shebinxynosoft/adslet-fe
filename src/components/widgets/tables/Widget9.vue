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
<!-- Button trigger modal -->


<!-- Modal -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h1 class="modal-title fs-5" id="exampleModalLabel">Create Tenants</h1>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
    <div class="mb-6">
  <label for="name" class="form-label">Name</label>
  <input type="text"  name="name" class="form-control" id="name"  placeholder="Enter Name">
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
  <input type="text" class="form-control" id="no_of_terminals" name="no_of_terminals" placeholder="name@example.com">
</div>
<div class="mb-3">
  <label for="phone_number" class="form-label">Phone Number</label>
  <input type="text" class="form-control" id="phone_number" name="phone_number"  placeholder="Phone Number">
</div>
<div class="mb-3">
  <label for="wallet" class="form-label"> Wallet</label>
  <input type="text" class="form-control" id="wallet" name="wallet" placeholder="Wallet">
</div>
<div class="mb-3">
  <label for="Address" class="form-label">Address</label>
  <textarea class="form-control" id="address"  name="address" rows="3"></textarea>
</div>

      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save</button>
      </div>
    </div>
  </div>
</div>
    <!--begin::Body-->
    <div class="card-body py-3">
      <!--begin::Table container-->
      <div class="table-responsive">
        <!--begin::Table-->
        <table
          class="table table-row-dashed table-row-gray-300 align-middle gs-0 gy-4"
        >
          <!--begin::Table head-->
          <thead>
            <tr class="fw-bold text-muted">
            
              <th>Name</th>
              <th>Slug</th>
              <th >Email</th>
              <th >No of Terminals</th>
              <th >Phone Number</th>
              <th >Wallet</th>
          
              <th>Actions</th>
            </tr>
          </thead>
          <!--end::Table head-->

          <!--begin::Table body-->
          <tbody>
            <template v-for="(item, index) in list" :key="index">
              <tr>
                <!-- <td>
                  <div
                    class="form-check form-check-sm form-check-custom form-check-solid"
                  >
                    <input
                      class="form-check-input widget-9-check"
                      type="checkbox"
                      :value="index"
                      v-model="checkedRows"
                    />
                  </div>
                </td> -->

                <td>
                  <div class="d-flex align-items-center">
                   
                    <div class="d-flex justify-content-start flex-column">
                      <a
                        href="#"
                        class="text-gray-900 fw-bold text-hover-primary fs-6"
                        >{{ item.name }}</a
                      >

                   
                    </div>
                  </div>
                </td>

                <td>
                  <a
                    href="#"
                    class="text-gray-900 fw-bold text-hover-primary d-block fs-6"
                    >{{ item.companyName }}</a
                  >
                 
                </td>

                <td class="text-end">
                  <div class="d-flex flex-column w-100 me-2">
                    <div class="d-flex flex-stack mb-2">
                      <span class="text-muted me-2 fs-7 fw-semibold">
                        {{ item.value }}%
                      </span>
                    </div>

                    <div class="progress h-6px w-100">
                      <div
                        class="progress-bar"
                        :class="`bg-${item.color}`"
                        role="progressbar"
                        :style="{ width: item.value + '%' }"
                        :aria-valuenow="item.value"
                        aria-valuemin="0"
                        aria-valuemax="100"
                      ></div>
                    </div>
                  </div>
                </td>
                <td>
                  <a
                    href="#"
                    class="text-gray-900 fw-bold text-hover-primary d-block fs-6"
                    >{{ item.companyName }}</a
                  >
                
                </td>
                <td>
                  <a
                    href="#"
                    class="text-gray-900 fw-bold text-hover-primary d-block fs-6"
                    >{{ item.companyName }}</a
                  >
               
                </td>
                <td>
                  <a
                    href="#"
                    class="text-gray-900 fw-bold text-hover-primary d-block fs-6"
                    >{{ item.companyName }}</a
                  >
                
                </td>
                <td class="text-end">
                  <a
                    href="#"
                    class="btn btn-icon btn-bg-light btn-active-color-primary btn-sm me-1"
                  >
                    <KTIcon icon-name="switch" icon-class="fs-3" />
                  </a>

                  <a
                    href="#"
                    class="btn btn-icon btn-bg-light btn-active-color-primary btn-sm me-1"
                  >
                    <KTIcon icon-name="pencil" icon-class="fs-3" />
                  </a>

                  <a
                    href="#"
                    class="btn btn-icon btn-bg-light btn-active-color-primary btn-sm"
                  >
                    <KTIcon icon-name="trash" icon-class="fs-3" />
                  </a>
                </td>
              </tr>
            </template>
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
import { getAssetPath } from "@/core/helpers/assets";
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "kt-widget-9",
  components: {},
  props: {
    widgetClasses: String,
  },
  setup() {
    const checkedRows = ref<Array<number>>([]);

    const list = [
      {
        image: getAssetPath("media/avatars/300-14.jpg"),
        name: "Ana Simmons",
        skills: "HTML, JS, ReactJS",
        companyName: "Intertico",
        companySkills: "Web, UI/UX Design",
        value: "50",
        color: "primary",
      },
      {
        image: getAssetPath("media/avatars/300-2.jpg"),
        name: "Jessie Clarcson",
        skills: "C#, ASP.NET, MS SQL",
        companyName: "Agoda",
        companySkills: "Houses & Hotels",
        value: "70",
        color: "danger",
      },
      {
        image: getAssetPath("media/avatars/300-5.jpg"),
        name: "Lebron Wayde",
        skills: "PHP, Laravel, VueJS",
        companyName: "RoadGee",
        companySkills: "Transportation",
        value: "60",
        color: "success",
      },
      {
        image: getAssetPath("media/avatars/300-20.jpg"),
        name: "Natali Goodwin",
        skills: "Python, PostgreSQL, ReactJS",
        companyName: "The Hill",
        companySkills: "Insurance",
        value: "50",
        color: "warning",
      },
      {
        image: getAssetPath("media/avatars/300-23.jpg"),
        name: "Kevin Leonard",
        skills: "HTML, JS, ReactJS",
        companyName: "RoadGee",
        companySkills: "Art Director",
        value: "90",
        color: "info",
      },
    ];

    return {
      list,
      checkedRows,
      getAssetPath,
    };
  },
});
</script>
