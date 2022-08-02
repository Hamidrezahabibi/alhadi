<template>
    <div class="card-student card" style="width: 18rem;">
        <div class="card-header">
            Student
        </div>
        <ul class="list-group list-group-flush">
            <li class="list-group-item">{{student.name}}</li>
            <li class="list-group-item">{{student.uni}}</li>
            <li class="list-group-item">{{student.age}}</li>
        </ul>
    </div>
</template>

<script>
export default {
    props: {
        student:{
            type: Object,
            required: true
        }
    },
    setup(props){
        console.log(props.student)
    }
}
</script>

<style>
.card-student {
    margin-left: 500px;
}
</style>

