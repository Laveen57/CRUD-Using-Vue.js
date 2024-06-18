<template>
    <div id="employee-form">
        <form @submit.prevent="handleSubmit">
            <label for="">Employee Name</label>
            <input type="text" 
            v-model="employee.name" 
            :class="{'has-error':submitting&&invalidName}"
            @focus="clearStatus"
            @keypress="clearStatus"
            ref="firstInput"
            >


            <label for="">Employee Email</label>
            <input type="text" 
            v-model="employee.email"
            :class="{'has-error':submitting&&invalidEmail}"
            @focus="clearStatus"
            @keypress="clearStatus"
            ref="secondInput"
            >

            <p v-if="submitting&&error" class="error-message">Please Fill out all the required fields!</p>
            <p v-if="success" class="success-message">Employee successfully added!</p>
            <button>Add Employee</button>
        </form>
    </div>
</template>

<script>
export default{
    name: 'employee-form',
    data(){
        return{
            submitting:false,
            success:false,
            error:false,
            employee:{
                name:'',
                email:''
            }
        }
    },
    methods:{
        handleSubmit(){
            this.submitting=true;
            this.clearStatus();
            if(this.invalidEmail||this.invalidName){
                this.error=true;
                return;
            }
            this.$emit('add:employee',this.employee);
            this.$refs.firstInput.focus(); 

            this.employee={
                name:'',
                email:''
            };
            this.success=true; 
            this.error=false;
            this.submitting=false;
        },
        clearStatus(){
            this.success=false;
            this.error=false;
        }
    },
    computed:{
        invalidName(){
            return this.employee.name==='';
        },
        invalidEmail(){
            return this.employee.email==='';
        }
    }
}
</script>

<style scoped>
form{
    margin-bottom: 2rem;
}
[class*='-message']{
    font-weight: 500;
}

.error-message{
    color: #d33c40;
}

.success-message{
    color: #32a95d;
}
</style>