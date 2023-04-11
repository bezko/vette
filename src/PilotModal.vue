<template>
    <div class = "modal-window">
        <ul>
            <li>Name: {{ pilot.name }}</li>
            <li>Height: {{ pilot.height }}</li>
            <li>Mass: {{ pilot.mass }}</li>
            <li>Hair Color: {{ pilot.hair_color }}</li>
            <li>Skin Color: {{ pilot.skin_color }}</li>
            <li>Eye Color: {{ pilot.eye_color }}</li>
            <li>Birth year: {{ pilot.birth_year }}</li>
            <li>Gender: {{ pilot.gender }}</li>
        </ul>
    </div>
</template>
<script>
    export default {
        props: {
            pilot: Object
        }
    }
</script>
<style>
.modal-container{    
    background-color: #444;
}
.modal-container li{
    color: #333;
    font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    font-size:36px;
    padding:18px;
} 
.modal-window{
    padding: 36px;
    background-color: white;
    border-radius: 12px;
}


</style>