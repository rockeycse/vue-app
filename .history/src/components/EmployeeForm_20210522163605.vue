<template>
  <div id="employee-form">
    <form @submit.prevent="handleSubmit">
      <label>Employee name</label>
      <input v-model="employee.name" type="text" />
      <label>Employee Email</label>
      <input v-model="employee.email" type="text" />
      <button>Add Employee</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "employee-form",
  computed: {
    invalidName() {
      return this.employee.name === "";
    },

    invalidEmail() {
      return this.employee.email === "";
    },
  },

  data() {
    return {
      submitting: false,
      error: false,
      success: false,
      employee: {
        name: "",
        email: "",
      },
    };
  },
  methods: {
    handleSubmit() {
    //   this.$emit("add:employee", this.employee);
    //   // console.log(this.employee);
    handleSubmit() {
    this.submitting = true
    this.clearStatus()

    if (this.invalidName || this.invalidEmail) {
      this.error = true
      return
    }

    this.$emit('add:employee', this.employee)
    this.employee = {
      name: '',
      email: '',
    }
    this.error = false
    this.success = true
    this.submitting = false
  },

  clearStatus() {
    this.success = false
    this.error = false
  }
    },
  },
};
</script>

<style scoped>
form {
  margin-bottom: 2rem;
}
</style>