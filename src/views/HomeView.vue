<template>
        <div class="form-box" v-if="isVisibility">
                <form @submit.prevent = "validation">
                    <div class="text-left">
                        <label for="title" class="form-group">Name</label>
                        <input type="text" class="form-control" id="title" v-model.lazy.trim="name" />
                        <small id="titleHelp" class="form-text text-danger">{{ nameError }}</small>
                    </div>
                    <br>
                    <br>
                    <div class="form-group text-left">
                        <label for="body">Uni</label>
                        <input type="text" class="form-control" v-model.lazy.trim="uni" />
                        <small id="bodyHelp" class="form-text text-danger">{{ uniError }}</small>
                    </div>
                    <br>
                    <br>
                    <div class="text-left">
                        <label for="title" class="form-group">Age</label>
                        <input type="number" class="form-control" id="title" v-model.lazy.trim="age" />
                        <small id="titleHelp" class="form-text text-danger">{{ ageError }}</small>
                    </div>
                    <br>
                    <br>
                    <button type="submit" class="btn btn-dark">
                        <div v-if="loading" class="spinner-border spinner-border-sm text-white" role="status" :disabled="loading">
                            <span class="sr-only"></span>
                        </div>
                        Creat Post
                    </button>
                </form>
        </div>
        <div v-if="isVisibility === false" v-for="(student, index) in students" :key="index" >
            <StudentView :student="student" />
        </div>
</template>

<script>
import { reactive, ref } from '@vue/reactivity'
import StudentView from './StudentView.vue'
export default {
    name: "create",
    components: {
        StudentView
    },
    setup() {
        const name = ref("");
        const uni = ref("");
        const age = ref(null);
        const nameError = ref("");
        const uniError = ref("");
        const ageError = ref("");
        let students = ref([]);
        const isVisibility = ref(true);
        //console.log(students.value)
        const loading = ref(false);
        function validation() {
            if (name.value === "") {
                nameError.value = "name is required";
            }
            else {
                nameError.value = "";
            }
            if (uni.value === "") {
                uniError.value = "uni is required";
            }
            else {
                uniError.value = "";
            }
            if (age.value === null) {
                ageError.value = "age is required";
            }
            else {
                ageError.value = "";
            }
            if (name.value !== "" && uni.value !== "" && age.value !== null) {
                isVisibility.value = false;
                loading.value = true;
                createStudent();
            }
        }
        function createStudent() {
            let student = {
                name: name.value,
                uni: uni.value,
                age: age.value,
            };
            students.value.push(student);
            console.log(students.value);
        }
        return { name, uni, age, nameError, uniError, ageError, students, loading, isVisibility, validation };
    },
    components: { StudentView }
}
</script>

<style>
.form-box{
  border: 1px solid rgb(2, 2, 2);
  padding: 40px;
  border-radius: 20px;
  margin-left: 350px;
  width: 500px;
}
</style>