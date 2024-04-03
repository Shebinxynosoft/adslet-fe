
<template>
    <!--begin::Tables Widget 9-->
    <div class="card" :class="widgetClasses">
      <!--begin::Header-->
      <div class="card-header border-0 pt-5">
        <h3 class="card-title align-items-start flex-column">
          <span class="card-label fw-bold fs-3 mb-1">Sms Campaign List</span>
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
            data-bs-target="#kt_modal_create_api_key"
          >
            <KTIcon icon-name="plus" icon-class="fs-3" />
            New Sms Campaign 
          </a>
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
                  <th>Name</th>
                  <th>Phone Number</th>   
                  <th>Description</th>
                  <th>Message</th>
                  <th>Start Date</th>
                  <th>End Date</th>
                </tr>
              </thead>
            <!--end::Table head-->
  
            <!--begin::Table body-->
            <tbody>
                <template v-for="(smscampaign, index) in smscampaigns" :key="index">
                  <tr>
                    <td>
                      <div class="d-flex align-items-center">
                        <div class="d-flex justify-content-start flex-column">
                          <a
                            href="#"
                            class="text-gray-900 fw-bold text-hover-primary fs-6"
                            >{{ smscampaign.name }}</a
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
                            >{{ smscampaign.phone_number }}</a
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
                            >{{ smscampaign.description }}</a
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
                            >{{ smscampaign.message }}</a
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
                            >{{ smscampaign.start_date }}</a
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
                            >{{ smscampaign.end_date }}</a
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
                        data-bs-toggle="modal"
                        data-bs-target="#kt_modal_new_branch1"
                        href="#"
                        class="btn btn-icon btn-bg-light btn-active-color-primary btn-sm me-1"
                        @click.prevent="">
                        <KTIcon icon-name="pencil" icon-class="fs-3" />
                    </a>
    
                      <a
                    href="#"
                    class="btn btn-icon btn-bg-light btn-active-color-primary btn-sm"
                    @click.prevent="deleteSmscampaign(smscampaign.id)"
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
  
      <!--begin::Modal - New Target-->
     
      <!--end::Modal - New Target-->
       <!--begin::Modal - New Target-->
     
      <!--end::Modal - New Target-->
    </div>
    <div
      class="modal fade"
      id="kt_modal_create_api_key"
      ref="createAPIKeyModalRef"
      tabindex="-1"
      aria-hidden="true"
    >
      <!--begin::Modal dialog-->
      <div class="modal-dialog modal-dialog-centered mw-650px">
        <!--begin::Modal content-->
        <div class="modal-content">
          <!--begin::Modal header-->
          <div class="modal-header" id="kt_modal_create_api_key_header">
            <!--begin::Modal title-->
            <h2>Create Sms Campaign</h2>
            <!--end::Modal title-->
  
            <!--begin::Close-->
            <div
              class="btn btn-sm btn-icon btn-active-color-primary"
              data-bs-dismiss="modal"
            >
              <KTIcon icon-name="cross" icon-class="fs-1" />
            </div>
            <!--end::Close-->
          </div>
          <!--end::Modal header-->
  
          <!--begin::Form-->
          <VForm
            id="kt_modal_create_api_key_form"
            class="form"
            @submit="submit"
            :validation-schema="validationSchema"
          >
            <!--begin::Modal body-->
            <div class="modal-body py-10 px-lg-17">
              <!--begin::Scroll-->
              <div
                class="scroll-y me-n7 pe-7"
                id="kt_modal_create_api_key_scroll"
                data-kt-scroll="true"
                data-kt-scroll-activate="{default: false, lg: true}"
                data-kt-scroll-max-height="auto"
                data-kt-scroll-dependencies="#kt_modal_create_api_key_header"
                data-kt-scroll-wrappers="#kt_modal_create_api_key_scroll"
                data-kt-scroll-offset="300px"
              >
              
  
                  <!--begin::Input group-->
                  <div class="mb-5 fv-row">
                  <!--begin::Label-->
                  <label class="required fs-5 fw-semibold mb-2">Name</label>
                  <!--end::Label-->
  
                  <!--begin::Input-->
                  <Field
                    type="text"
                    class="form-control form-control-solid"
                    placeholder="Name"
                    name="name"
                    v-model="smscampaignData.name"
                  />
                  <div class="fv-plugins-message-container">
                    <div class="fv-help-block">
                      <ErrorMessage name="name" />
                    </div>
                  </div>
                  <!--end::Input-->
                  
                </div>
                
                  <!--begin::Input group-->
                  <div class="mb-5 fv-row">
    <!--begin::Label-->
    <label class="required fs-5 fw-semibold mb-2">Phone Numbers</label>
    <!--end::Label-->

    <!--begin::Textarea-->
    <Field
        as="textarea"
        class="form-control form-control-solid"
        placeholder="Enter Phone Numbers (separated by comma, semicolon, or space)"
        name="phone_number"
        v-model="smscampaignData.phone_number"
        rows="4"
    />
    <div class="fv-plugins-message-container">
        <div class="fv-help-block">
            <ErrorMessage name="phone_number" />
        </div>
    </div>
    <!--end::Textarea-->
</div>
                 
              
                 <!--begin::Input group-->
                <div class="mb-5 fv-row">
              <!--begin::Label-->
              <label class="required fs-5 fw-semibold mb-2">Description</label>
              <!--end::Label-->
              <!--begin::Textarea-->
              <Field
                as="textarea"
                class="form-control form-control-solid"
                placeholder="Enter description"
                name="description"
                v-model="smscampaignData.description"
                rows="3"
              />
              <div class="fv-plugins-message-container">
                <div class="fv-help-block">
                  <ErrorMessage name="description" />
                </div>
              </div>
              <!--end::Textarea-->
            </div>
            <div class="mb-5 fv-row">
              <!--begin::Label-->
              <label class="required fs-5 fw-semibold mb-2">Message</label>
              <!--end::Label-->
              <!--begin::Textarea-->
              <Field
                as="textarea"
                class="form-control form-control-solid"
                placeholder="Enter Message"
                name="message"
                v-model="smscampaignData.message"
                rows="3"
              />
              <div class="fv-plugins-message-container">
                <div class="fv-help-block">
                  <ErrorMessage name="message" />
                </div>
              </div>
              <!--end::Textarea-->
            </div>
            <div class="mb-5 fv-row">
                  <!--begin::Label-->
                  <label class="required fs-5 fw-semibold mb-2">Start Date</label>
                  <!--end::Label-->
  
                  <!--begin::Input-->
                  <Field
                    type="date"
                    class="form-control form-control-solid"
                    placeholder="Start Date"
                    name="start_date"
                    v-model="smscampaignData.start_date"
                  />
                  <div class="fv-plugins-message-container">
                    <div class="fv-help-block">
                      <ErrorMessage name="start_date" />
                    </div>
                  </div>
                  <!--end::Input-->
                  
                </div>
                <div class="mb-5 fv-row">
                  <!--begin::Label-->
                  <label class="required fs-5 fw-semibold mb-2">End Date</label>
                  <!--end::Label-->
  
                  <!--begin::Input-->
                  <Field
                    type="date"
                    class="form-control form-control-solid"
                    placeholder="Role Name"
                    name="end_date"
                    v-model="smscampaignData.end_date"
                  />
                  <div class="fv-plugins-message-container">
                    <div class="fv-help-block">
                      <ErrorMessage name="end_date" />
                    </div>
                  </div>
                  <!--end::Input-->
                  
                </div>
              
          
  
              </div>
              <!--end::Scroll-->
            </div>
            <!--end::Modal body-->
  
            <!--begin::Modal footer-->
            <div class="modal-footer flex-center">
              <!--begin::Button-->
              <button
                type="reset"
                id="kt_modal_create_api_key_cancel"
                class="btn btn-light me-3"
              >
                Discard
              </button>
              <!--end::Button-->
  
              <!--begin::Button-->
              <button
                ref="submitButtonRef"
                type="submit"
                id="kt_modal_create_api_key_submit"
                class="btn btn-primary"
              >
                <span class="indicator-label"> Submit </span>
                <span class="indicator-progress">
                  Please wait...
                  <span
                    class="spinner-border spinner-border-sm align-middle ms-2"
                  ></span>
                </span>
              </button>
              <!--end::Button-->
            </div>
            <!--end::Modal footer-->
          </VForm>
          <!--end::Form-->
        </div>
        <!--end::Modal content-->
      </div>
      <!--end::Modal dialog-->
    </div>
  </template>
  <script lang="ts">
  import { getAssetPath } from "@/core/helpers/assets";
  import { defineComponent, ref, onMounted, reactive, computed } from "vue";
  import { hideModal } from "@/core/helpers/modal";
  import { ErrorMessage, Field, Form as VForm } from "vee-validate";
  import * as Yup from "yup";
  import Swal from "sweetalert2/dist/sweetalert2.js";
  import ApiService from "@/core/services/ApiService";
  
  interface SmsCampaign {
    id: number;
    name: string;
    phone_number: string; 
    description: string;
    message: string;
    start_date: string;
    end_date: string;

  }
  
  export default defineComponent({
    name: "create-api-key-modal",
    components: {
      ErrorMessage,
      Field,
      VForm,
    },
    setup() {
      const submitButtonRef = ref<null | HTMLButtonElement>(null);
      const modalRef = ref<null | HTMLElement>(null);
      const createAPIKeyModalRef = ref<null | HTMLElement>(null);
  
      const smscampaigns = ref<SmsCampaign[]>([]);
      const smscampaignData = reactive({
        name: "",
        phone_number: "",
        description: "",
        message: "",
        start_date: "",
        end_date: "",
       
        
      });
      const validationSchema = Yup.object().shape({
        name: Yup.string().required().label("Name"),
        phone_number: Yup.string().required().label("Phone number"),
        description: Yup.string().required().label("Description"),
        message: Yup.string().required().label("Message"),
        start_date: Yup.string().required().label("Date"),
        end_date: Yup.string().required().label("Date"),
  
      });
  
      const loading = ref(false);
  
      const fetcheSmscampaigns = () => {
        loading.value = true;
        ApiService.get("http://localhost:8000/api/smscampaigns")
          .then((response) => {
            smscampaigns.value = response.data.data as SmsCampaign[];
            console.log("Fetched SmsCampaigns:", smscampaigns.value);
          })
          .catch((error) => {
            console.error("Error fetching SmsCampaigns:", error);
            Swal.fire({
              text: "Failed to fetch SmsCampaigns. Please try again later.",
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
      onMounted(fetcheSmscampaigns);
  
      const submit = () => {
        if (!submitButtonRef.value) {
          return false;
        }
        // Disable button
        submitButtonRef.value.disabled = true;
        // Activate indicator
        submitButtonRef.value.setAttribute("data-kt-indicator", "on");
  
        // Assuming loading is a reactive variable
        loading.value = true; // Set loading to true while submitting
  
        return new Promise((resolve, reject) => {
          setTimeout(() => {
            ApiService.post("http://localhost:8000/api/smscampaigns", smscampaignData)
              .then((response) => {
                console.log("SmsCampaigns created:", response.data);
                Swal.fire({
                  text: "SmsCampaigns created successfully!",
                  icon: "success",
                  buttonsStyling: false,
                  confirmButtonText: "Ok, got it!",
                  heightAuto: false,
                  customClass: {
                    confirmButton: "btn fw-semibold btn-light-primary",
                  },
                }).then(() => {
                  hideModal(createAPIKeyModalRef.value);
                });
                resolve(true); // Resolve the promise with true indicating success
              })
              .catch((error) => {
                console.error("Error creating SmsCampaigns:", error);
                Swal.fire({
                  text: "Failed to create SmsCampaigns. Please try again later.",
                  icon: "error",
                  buttonsStyling: false,
                  confirmButtonText: "Ok, got it!",
                  heightAuto: false,
                  customClass: {
                    confirmButton: "btn fw-semibold btn-light-danger",
                  },
                });
                reject(false); // Reject the promise with false indicating failure
              })
              .finally(() => {
                // Reset loading after submission
                loading.value = false;
                if (submitButtonRef.value) {
                  submitButtonRef.value.disabled = false;
                  submitButtonRef.value?.removeAttribute("data-kt-indicator");
                }
              });
          }, 2000);
        });
      };
  
      const deleteSmscampaign = (id: number) => {
        loading.value = true;
        ApiService.delete(`http://localhost:8000/api/smscampaigns/${id}`)
          .then(() => {
            // After successful deletion, fetch roles again to refresh the list
            fetcheSmscampaigns();
            Swal.fire({
              text: "SmsCampaigns deleted successfully!",
              icon: "success",
              buttonsStyling: false,
              confirmButtonText: "Ok, got it!",
              heightAuto: false,
              customClass: {
                confirmButton: "btn fw-semibold btn-light-primary",
              },
            });
          })
          .catch((error) => {
            console.error("Error deleting SmsCampaigns:", error);
            Swal.fire({
              text: "Failed to delete SmsCampaigns. Please try again later.",
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
  
      // Fetch roles on component mount
      onMounted(fetcheSmscampaigns);
  
      // Define the widgetClasses computed property
      const widgetClasses = computed(() => ({
        'card': true,
        'card-custom': true,
        'card-stretch': true,
        // Add more classes as needed
      }));
  
      return {
        smscampaignData,
        validationSchema,
        submit,
        deleteSmscampaign,
        smscampaigns,
        submitButtonRef,
        modalRef,
        createAPIKeyModalRef,
        getAssetPath,
        widgetClasses,
      };
    },
  });
  </script>
  
  
  
  
  
  