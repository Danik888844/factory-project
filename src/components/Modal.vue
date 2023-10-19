<template>
  <div class="backdrop" @click.self="closeModal">
    <div class="modal">
        <h2>Добавление фабрики в cookie</h2>
        <form>
            <label>Город: </label>
            <select @change="getGilds" v-model="city">
                <option v-for="city in cities" :key="city.id" :value="city">{{ city.CityName }}</option>
            </select>
            <label>Цех: </label>
            <select @change="getEmployees" v-model="gild">
                <option v-for="gild in gilds" :key="gild.id" :value="gild">{{ gild.GildName }}</option>
            </select>
            <label>Работник: </label>
            <select>
                <option v-for="employee in employees" :key="employee.id" :value="employee.id">{{ employee.FullName }}</option>
            </select>
            <label>Бригада: </label>
            <select required>
                <option v-for="brigade in birages" :key="brigade.id" :value="brigade.id">{{ brigade.BrigadeName }}</option>
            </select>
            <label>Смена: </label>
            <select required>
                <option v-for="shift in shifts" :key="shift.id" :value="shift.id">{{ shift.ShiftName }}</option>
            </select>

            <input type="submit" style="margin-top: 25px;" />
        </form>
    </div>
  </div>
</template>

<script>
export default {
    data(){
        return{
            city: null,
            gild: null,
            gilds: [],
            employees: [],
            brigades: [],
            shifts: []
        }
    },
    props: ['cities'],
    methods: {
        closeModal(){
            this.$emit('close')
        },
        getGilds(){
            if(!this.city)
                return null;

            this.gilds = []
            this.employees = []
            for (const gildId of this.city.Gilds){
                fetch('http://localhost:3000/gilds/'+gildId)
                .then((res)=>res.json())
                .then(data => this.gilds.push(data))
                .catch(err => console.log(err.message))
            }
        },
        getEmployees(){
            if(!this.gild)
                return null;

            this.employees = []
            for (const employeeId of this.gild.Employees){
                fetch('http://localhost:3000/employees/'+employeeId)
                .then((res)=>res.json())
                .then(data => this.employees.push(data))
                .catch(err => console.log(err.message))
            }
        }
    }
}
</script>

<style>
    .modal {
        max-width: 600px;
        max-height: 500px;
        padding: 20px;
        margin: 100px auto;
        background: white;
        border-radius: 5px;
        overflow: auto;
    }
    .backdrop {
        top: 0;
        position: fixed;
        background: rgba(0,0,0,0.5);
        width: 100%;
        height: 100%;
    }
</style>