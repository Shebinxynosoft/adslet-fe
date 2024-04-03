<template>
    <!--begin::Tables Widget 9-->
    <div class="card" :class="widgetClasses">
      <!--begin::Header-->
      <div class="card-header border-0 pt-5">
        <h3 class="card-title align-items-start flex-column">
          <span class="card-label fw-bold fs-3 mb-1">Roles List</span>
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
            New Roles
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
                <th>Actions</th>
              </tr>
            </thead>
            <!--end::Table head-->
  
            <!--begin::Table body-->
            <tbody>
              <template v-for="(role, index) in roles" :key="index">
                <tr>
                  <td>
                    <div class="d-flex align-items-center">
                      <div class="d-flex justify-content-start flex-column">
                        <a
                          href="#"
                          class="text-gray-900 fw-bold text-hover-primary fs-6"
                          >{{ role.name }}</a
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
                      data-bs-target="#kt_modal_new_target1"
                      href="#"
                      class="btn btn-icon btn-bg-light btn-active-color-primary btn-sm me-1"
                      @click.prevent="editRole(role.id)">
                      <KTIcon icon-name="pencil" icon-class="fs-3" />
                  </a>
  
                    <a
                  href="#"
                  class="btn btn-icon btn-bg-light btn-active-color-primary btn-sm"
                  @click.prevent="deleteRole(role.id)"
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
     </div>
    <!--end::Tables Widget 9-->

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
          <h2>Create Role</h2>
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
                <label class="required fs-5 fw-semibold mb-2">Role</label>
                <!--end::Label-->

                <!--begin::Input-->
                <Field
                  type="text"
                  class="form-control form-control-solid"
                  placeholder="Role Name"
                  name="name"
                  v-model="roleData.name"
                />
                <div class="fv-plugins-message-container">
                  <div class="fv-help-block">
                    <ErrorMessage name="Role Name" />
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
  import { defineComponent, ref, onMounted,reactive } from "vue";
  import { hideModal } from "@/core/helpers/modal";
  import { ErrorMessage, Field, Form as VForm } from "vee-validate";
  import * as Yup from "yup";
  import Swal from "sweetalert2/dist/sweetalert2.js";
  import ApiService from "@/core/services/ApiService";
  
  interface Role {
    id: number;
    name: string;
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
      
      const roles = ref<Role[]>([]);
      const roleData = reactive({
      name: "",
      });
      const validationSchema = Yup.object().shape({
      name: Yup.string().required().label("name"),
      });
  
      const loading = ref(false);
    
    const fetchRoles = () => {
      loading.value = true;
      ApiService.get("http://localhost:8000/api/roles")
        .then((response) => {
          roles.value = response.data.data as Role[]; 
          console.log("Fetched roles:", roles.value);
        })
        .catch((error) => {
          console.error("Error fetching roles:", error);
          Swal.fire({
            text: "Failed to fetch roles. Please try again later.",
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
    onMounted(fetchRoles);

const submit = () => {
  if (!submitButtonRef.value) {
    return false;
  }
  // Disable button
  submitButtonRef.value.disabled = true;
  // Activate indicator
  submitButtonRef.value.setAttribute("data-kt-indicator", "on");

  // Assuming targetData is defined somewhere
  // Assuming loading is a reactive variable
  loading.value = true; // Set loading to true while submitting

  return new Promise((resolve, reject) => {
    setTimeout(() => {
      ApiService.post("http://localhost:8000/api/roles", roleData)
        .then((response) => {
          console.log("Role created:", response.data);
          Swal.fire({
            text: "Role created successfully!",
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
          console.error("Error creating role:", error);
          Swal.fire({
            text: "Failed to create role. Please try again later.",
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
const deleteRole = (id: number) => {
      loading.value = true;
      ApiService.delete(`http://localhost:8000/api/roles/${id}`)
        .then(() => {
          // After successful deletion, fetch roles again to refresh the list
          fetchRoles();
          Swal.fire({
            text: "Role deleted successfully!",
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
          console.error("Error deleting role:", error);
          Swal.fire({
            text: "Failed to delete role. Please try again later.",
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
    onMounted(fetchRoles);
      return {
        roleData,
        validationSchema,
        submit,
        deleteRole,
        roles,
        submitButtonRef,
        modalRef,
        createAPIKeyModalRef,
        getAssetPath,
      };
    },
  });
  </script>