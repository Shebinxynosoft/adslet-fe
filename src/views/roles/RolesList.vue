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
          data-bs-target="#kt_modal_new_target"
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
    <!--begin::Body-->

    <!--begin::Modal - New Target-->
    <div
      class="modal fade"
      id="kt_modal_new_target"
      ref="newTargetModalRef"
      tabindex="-1"
      aria-hidden="true"
    >
      <!--begin::Modal dialog-->
      <div class="modal-dialog modal-dialog-centered mw-650px">
        <!--begin::Modal content-->
        <div class="modal-content rounded">
          <!--begin::Modal header-->
          <div class="modal-header pb-0 border-0 justify-content-end">
            <!--begin::Close-->
            <div
              class="btn btn-sm btn-icon btn-active-color-primary"
              data-bs-dismiss="modal"
            >
              <KTIcon icon-name="cross" icon-class="fs-1" />
            </div>
            <!--end::Close-->
          </div>
          <!--begin::Modal header-->

          <!--begin::Modal body-->
          <div class="modal-body scroll-y px-10 px-lg-15 pt-0 pb-15">
          <!--begin:Form-->
          <el-form
            id="kt_modal_new_target_form"
            @submit.prevent="submit()"
            :model="targetData"
            :rules="rules"
            ref="formRef"
            class="form"
          >
            <!--begin::Heading-->
            <div class="mb-13 text-center">
              <!--begin::Title-->
              <h1 class="mb-3">Add Roles</h1>
              <!--end::Title-->

              
              <!--end::Description-->
            </div>
            <!--end::Heading-->

            <!--begin::Input group-->
            <div class="d-flex flex-column mb-8 fv-row">
              <!--begin::Label-->
              <label class="d-flex align-items-center fs-6 fw-semibold mb-2">
                <span class="required">Role Name</span>
              </label>
              <!--end::Label-->

              <el-form-item prop="name">
                <el-input
                  v-model="targetData.name"
                  placeholder="Enter Role Name"
                  name="name"
                ></el-input>
              </el-form-item>
            </div>
            <!--end::Input group-->

            <!--end::Input group-->

           
            <!--begin::Actions-->
            <div class="text-center">
              <button
                type="reset"
                id="kt_modal_new_target_cancel"
                class="btn btn-light me-3"
              >
                Cancel
              </button>

              <!--begin::Button-->
              <button
                :data-kt-indicator="loading ? 'on' : null"
                class="btn btn-lg btn-primary"
                type="submit"
              >
                <span v-if="!loading" class="indicator-label">
                  Submit
                  <KTIcon icon-name="arrow-right" icon-class="fs-3 ms-2 me-0" />
                </span>
                <span v-if="loading" class="indicator-progress">
                  Please wait...
                  <span
                    class="spinner-border spinner-border-sm align-middle ms-2"
                  ></span>
                </span>
              </button>
              <!--end::Button-->
            </div>
            <!--end::Actions-->
          </el-form>
          <!--end:Form-->
        </div>
        <!--end::Modal body-->

     
        </div>
        <!--end::Modal content-->
      </div>
      <!--end::Modal dialog-->
    </div>
    <!--end::Modal - New Target-->
     <!--begin::Modal - New Target-->
     <div
      class="modal fade"
      id="kt_modal_new_target1"
      ref="newTargetModalRef"
      tabindex="-1"
      aria-hidden="true"
    >
      <!--begin::Modal dialog-->
      <div class="modal-dialog modal-dialog-centered mw-650px">
        <!--begin::Modal content-->
        <div class="modal-content rounded">
          <!--begin::Modal header-->
          <div class="modal-header pb-0 border-0 justify-content-end">
            <!--begin::Close-->
            <div
              class="btn btn-sm btn-icon btn-active-color-primary"
              data-bs-dismiss="modal"
            >
              <KTIcon icon-name="cross" icon-class="fs-1" />
            </div>
            <!--end::Close-->
          </div>
          <!--begin::Modal header-->

          <!--begin::Modal body-->
          <div class="modal-body scroll-y px-10 px-lg-15 pt-0 pb-15">
          <!--begin:Form-->
          <el-form
            id="kt_modal_new_target_form"
            @submit.prevent="submit()"
            :model="targetData"
            :rules="rules"
            ref="formRef"
            class="form"
          >
            <!--begin::Heading-->
            <div class="mb-13 text-center">
              <!--begin::Title-->
              <h1 class="mb-3">Edit Roles</h1>
              <!--end::Title-->

              
              <!--end::Description-->
            </div>
            <!--end::Heading-->

            <!--begin::Input group-->
            <div class="d-flex flex-column mb-8 fv-row">
              <!--begin::Label-->
              <label class="d-flex align-items-center fs-6 fw-semibold mb-2">
                <span class="required">Role Name</span>
              </label>
              <!--end::Label-->

              <el-form-item prop="name">
    <el-input
        v-model="targetData.name"
        placeholder="Enter Role Name"
        name="name"
        :value="(role as any).name"
      ></el-input>
   </el-form-item>
            </div>
            <!--end::Input group-->

            <!--end::Input group-->

           
            <!--begin::Actions-->
            <div class="text-center">
              <button
                type="reset"
                id="kt_modal_new_target_cancel"
                class="btn btn-light me-3"
              >
                Cancel
              </button>

              <!--begin::Button-->
              <button
                :data-kt-indicator="loading ? 'on' : null"
                class="btn btn-lg btn-primary"
                type="submit"
              >
                <span v-if="!loading" class="indicator-label">
                  Submit
                  <KTIcon icon-name="arrow-right" icon-class="fs-3 ms-2 me-0" />
                </span>
                <span v-if="loading" class="indicator-progress">
                  Please wait...
                  <span
                    class="spinner-border spinner-border-sm align-middle ms-2"
                  ></span>
                </span>
              </button>
              <!--end::Button-->
            </div>
            <!--end::Actions-->
          </el-form>
          <!--end:Form-->
        </div>
        <!--end::Modal body-->

     
        </div>
        <!--end::Modal content-->
      </div>
      <!--end::Modal dialog-->
    </div>
    <!--end::Modal - New Target-->
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
interface Role {
  id: number;
  name: string;
 
}

export default defineComponent({
  name: "kt-widget-9",
  components: {},
  props: {
    widgetClasses: String,
  },
  data() {
    return {
      role: {}, // Initialize role object
      // Other data properties
    };
  },
  setup() {
    const roles = ref<Role[]>([]);
    const checkedRows = ref<Array<number>>([]);
    const targetData = reactive({
      name: "",
    });

    const rules = {
      name: [
        {
          required: true,
          message: "Role name is required",
          trigger: "blur",
        },
      ],
    };

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

    // Fetch roles on component mount
    onMounted(fetchRoles);

    const submit = () => {
      loading.value = true; // Set loading to true while submitting

      // Assuming ApiService has a method to post role data
      ApiService.post("http://localhost:8000/api/roles", targetData)
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
          });
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
        })
        .finally(() => {
          loading.value = false; // Reset loading after submission
        });
    };

    const editRole = (id: number) => {
    loading.value = true;
    ApiService.get(`http://localhost:8000/api/roles/${id}`)
    .then((response: { data: { id: number, name: string } }) => {
        // Access response data safely
   
            // Once the role is successfully edited, you may want to update the roles list
            fetchRoles();
            console.log("Role edited successfully!");
            Swal.fire({
                text: "Role edited successfully!",
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
            console.error("Error editing role:", error);
            Swal.fire({
                text: "Failed to edit role. Please try again later.",
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
      checkedRows,  
      roles,  
      editRole,
      deleteRole,
      targetData,
      rules,
      loading,
      submit,
    };
  },
});
</script>