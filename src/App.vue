<template>
  <div class="small-container">
    <h1>Employees</h1>
    <employee-form @add:employee="addEmployee"/>
    <employee-table 
    :employees="employees" 
    @delete:employee="deleteEmployee"
    @edit:employee="editEmployee"
    />

  </div>
 
</template>

<script>
import EmployeeTable from './components/EmployeeTable.vue'
import EmployeeForm from './components/EmployeeForm.vue'

export default {
  name: 'App',
  components: {
    EmployeeTable,
    EmployeeForm 
  },
  data(){
    return{
      employees:[
        {
          id: 1,
          name: 'Laveenkumar L',
          email: 'laveen.lokesh0507@gmail.com'
        },
        {
          id: 2,
          name: 'Srinivas V',
          email: 'srinivasvenugopal56@gmail.com'
        },
        {
          id: 3,
          name: 'Kiran C',
          email: 'kiranreddy107@gmail.com'
        }
      ]
    }
  },
  methods:{
    addEmployee(employee){
      const lastId = this.employees.length>0?this.employees[this.employees.length-1].id:0;
      
      const id = lastId + 1;

      const newEmployee = {...employee,id}

      this.employees = [...this.employees,newEmployee];
    },
    deleteEmployee(id){
      this.employees=this.employees.filter((employee)=>{
        return employee.id!=id;
      })
    },
    editEmployee(id,updatedEmployee){
      this.employees.map((employee)=>{
        return employee.id==id?updatedEmployee:employee;
      })
    }
  }
}
</script>

<style>
button{
  background: #009435;
  border: 1px solid #009435;
}

.small-container {
  max-width: 680px;
}

</style>
