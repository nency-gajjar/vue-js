<template>
    <div id="employee-table">
    <p v-if="employees.length < 1" class="empty-table">
    No employees
    </p>    
    <table v-else>
      <thead>
        <tr>
          <th>Employee name</th>
          <th>Employee email</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="employee in employees" :key="employee.id">
          <td>{{ employee.name }}</td>
          <td>{{ employee.email }}</td>
          <td>
            <button @click="editMode(employee.id)">Edit</button>
            <button @click="$emit('delete:employee', employee.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
    </div>
</template>

<script>
export default {
    name : 'employee-table',
    props: {
        employees : Array ,
    },

    data() {
        return {
            editing: null,
    }
        },

    methods: {
        editMode(id) {
            this.editing = id
        },

        editEmployee(employee) {
            if (employee.name === '' || employee.email === '') return
            this.$emit('edit:employee', employee.id, employee)
            this.editing = null
        }
    }
}
</script>

<style scoped>
    button {
    margin: 0 0.5rem 0 0;
  }
</style>