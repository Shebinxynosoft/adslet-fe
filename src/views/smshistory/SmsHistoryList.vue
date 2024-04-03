<template>
    <!--begin::Tables Widget 9-->
    <div class="card" :class="widgetClasses">
      <!--begin::Header-->
      <div class="card-header border-0 pt-5">
        <h3 class="card-title align-items-start flex-column">
          <span class="card-label fw-bold fs-3 mb-1">Sms History List</span>
        </h3>
        <div
          class="card-toolbar"
          data-bs-toggle="tooltip"
          data-bs-placement="top"
          data-bs-trigger="hover"
          title="Click to add a user"
        >
          <!-- <a
            href="#"
            class="btn btn-sm btn-light-primary"
            data-bs-toggle="modal"
            data-bs-target="#kt_modal_new_question"
          >
            <KTIcon icon-name="plus" icon-class="fs-3" />
            New Questions
          </a> -->
        </div>
      </div>
      <!--end::Header-->
  
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
                <!-- <th>Tenant Sms Id</th> -->
                <th>Tenant ID</th>
                <th>Msg Length</th>
                <th>Msg Count</th>       
                <th>Msg Price</th>
                <th>Phone Number</th>
                <th>Text Message</th>
                <th>Msg Type</th>       
               
                           
                <!-- <th>Actions</th> -->
              </tr>
            </thead>
            <!--end::Table head-->
         
       
            <!--begin::Table body-->
            <tbody>
              <template v-for="(smshistory, index) in smshistories" :key="index">
                <tr>
                  <!-- <td>
                    <div class="d-flex align-items-center">
                      <div class="d-flex justify-content-start flex-column">
                        <a
                          href="#"
                          class="text-gray-900 fw-bold text-hover-primary fs-6"
                          >{{ smshistory.tenantsms_id }}</a
                        >
                      </div>
                    </div>
                  </td> -->
                  <td> 
      
                    <div class="d-flex align-items-center">
                      <div class="d-flex justify-content-start flex-column">
                        <a
                          href="#"
                          class="text-gray-900 fw-bold text-hover-primary fs-6"
                          >{{ smshistory.tenant_id }}</a
                        >
                      </div>
                    </div>
                  </td>
                  <td>
                    <div class="d-flex align-items-center">
                      <div class="d-flex justify-content-start flex-column">
                        <a
                          href="#"
                          class="text-gray-900 fw-bold text-hover-primary fs-6"
                          >{{ smshistory.msg_length }} </a
                        >
                      </div>
                    </div>
                  </td>
             
                  <td>
                    <div class="d-flex align-items-center">
                      <div class="d-flex justify-content-start flex-column">
                        <a
                          href="#"
                          class="text-gray-900 fw-bold text-hover-primary fs-6"
                          >{{ smshistory.msg_count }}</a
                        >
                      </div>
                    </div>
                  </td>
                  <td>
                    <div class="d-flex align-items-center">
                      <div class="d-flex justify-content-start flex-column">
                        <a
                          href="#"
                          class="text-gray-900 fw-bold text-hover-primary fs-6"
                          >{{ smshistory.msg_price }}</a
                        >
                      </div>
                    </div>
                  </td>
                  <td>
                    <div class="d-flex align-items-center">
                      <div class="d-flex justify-content-start flex-column">
                        <a
                          href="#"
                          class="text-gray-900 fw-bold text-hover-primary fs-6"
                          >{{ smshistory.phonenumber }}</a
                        >
                      </div>
                    </div>
                  </td>
                  <td>
                    <div class="d-flex align-items-center">
                      <div class="d-flex justify-content-start flex-column">
                        <a
                          href="#"
                          class="text-gray-900 fw-bold text-hover-primary fs-6"
                          >{{ smshistory.textmessage }}</a
                        >
                      </div>
                    </div>
                  </td>
                  <td>
                    <div class="d-flex align-items-center">
                      <div class="d-flex justify-content-start flex-column">
                        <a
                          href="#"
                          class="text-gray-900 fw-bold text-hover-primary fs-6"
                          >{{ smshistory.msg_type }}</a
                        >
                      </div>
                    </div>
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
     
    </div>
    <!--end::Tables Widget 9-->
  </template>
  
  <script lang="ts">
  import { getAssetPath } from "@/core/helpers/assets";
  import { defineComponent, ref, reactive,onMounted } from "vue";
  import ApiService from "@/core/services/ApiService";
  import JwtService from "@/core/services/JwtService";
  import { ErrorMessage, Field, Form as VForm } from "vee-validate";
  import { useRouter } from "vue-router";
  import Swal from "sweetalert2/dist/sweetalert2.js";
  import * as Yup from "yup";
  interface SmsHistory {
  
  id: number;
  tenant_id:string,
  tenantsms_id:string,
  msg_length:string,
  msg_count:string,
  msg_price:string,
  phonenumber:string,
  textmessage:string,
  msg_type:string,
}

  
  
  export default defineComponent({
    name: "kt-widget-9",
    components: {},
    props: {
      widgetClasses: String,
    },
    data() {
      return {
  // Initialize role object
        // Other data properties
      };
    },
    setup() {
      const smshistories = ref<SmsHistory[]>([]); // Change from 'roles' to 'tenants'
      const checkedRows = ref<number[]>([]); // Fixed the type declaration
      const smshistoryData = reactive({
       
        id: "",
      tenant_id:"",
      tenantsms_id:"",
      msg_length:"",
      msg_count:"",
      msg_price:"",
      phonenumber:"",
      textmessage:"",
      msg_type:"",
      
      });
  
      const rules = {
       
      };
  
      const loading = ref(false);
      
      const fetchSmshitory = () => { 
        loading.value = true;
        ApiService.get("http://localhost:8000/api/smshistory")
          .then((response) => {
            smshistories.value = response.data.data as SmsHistory[]; 
            console.log("Fetched smshistories:", smshistories.value); // Updated log message
          })
          .catch((error) => {
            console.error("Error fetching smshistories:", error); // Updated error message
            Swal.fire({
              text: "Failed to fetch smshistories. Please try again later.", // Updated error message
              icon: "error",
              buttonsStyling: false,
              confirmButtonText: "Ok, got it!",
              heightAuto: false,
              customClass: {
                confirmButton: "btn fw-semibold btn-light-danger",
              },
            });
          })
          .finally(() => {
            loading.value = false;
          });
      };
  
      onMounted(fetchSmshitory);
  
  
     
      return {
        checkedRows,  
        smshistories,
        smshistoryData,
        rules,
        loading,
      
      };
    },
  });
  </script>