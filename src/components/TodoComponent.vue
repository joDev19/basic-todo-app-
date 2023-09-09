<template>
    <div class="container">
        <div class="row">
            <h2>todo list</h2>
            <ul class="list-group">
                <li class="list-group-item list-group-item-action active">
                    <strong class="">Your Tasks</strong> 
                    <span class="float-end"><i class="fa-solid fa-square-plus fa-lg"></i></span>
                </li>
                <li class="list-group-item">
                    <input class="form-check-input me-1 mb-1 float-start" type="checkbox" value="" aria-label="...">
                    <span class="float-start">First checkbox</span>
                    <span class="float-end"><i class="fa-solid text-danger fa-circle-minus"></i></span>
                    <input type="text" class="form-control" name="" id="">
                </li>
            </ul>
        </div>
    </div>
</template>
<style scoped>
h2{
    text-transform: capitalize;
}
</style>
<script>
export default {

}
</script>