<template>
    <!--begin::Tables Widget 9-->
    <div class="card" :class="widgetClasses">
      <!--begin::Header-->
      <div class="card-header border-0 pt-5">
        <h3 class="card-title align-items-start flex-column">
          <span class="card-label fw-bold fs-3 mb-1">Roles</span>
  
        
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
            
                <th>Actions</th>
              </tr>
            </thead>
            <!--end::Table head-->
  
            <!--begin::Table body-->
            <tbody>
              <template v-for="(item, index) in list" :key="index">
                <tr>
        
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
  