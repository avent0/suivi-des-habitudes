<template>
    <div class="habitForm__content">
        <div class="habit_formBox">
            <div class="habit_form_title">
                <h4>Add a new habit</h4>
                <div class="close" @click="closeButton()">X</div>
            </div>
            <div class="addHabit_form_box">
                <form action="" @submit.prevent>
                    <div class="input_field">
                        <label for="">Nom habitude : </label><br>
                        <input type="text" v-model="habitudesData.nom_habitude">
                    </div>
                    <div class="input_field">
                        <label for="">Description habitude: </label><br>
                        <input type="text" v-model="habitudesData.description">
                    </div>
                    <div class="input_field">
                        <label for="">Description habitude: </label><br>
                        <select name="" id="" v-model="habitudesData.frequence">
                            <option value="quotidienne">quotidienne</option>
                            <option value="hebdomadaire">hebdomadaire</option>
                            <option value="mensuelle">Mensuelle</option>
                        </select>
                    </div>
                    <div class="input_field">
                        <label for="">Heure: </label>
                        <input type="time" v-model="habitudesData.heure_execution">
                    </div>
                    <div class="input_field">
                        <input @click="insertHabitude" type="submit" value="Send" id="submit">
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<script lang="ts" setup>
import {ref} from "vue"
import router from "@/router"
import { storeToRefs } from "pinia"
const { habitudes } = storeToRefs(useHabitudeStore())
import { useHabitudeStore } from '@/stores/habitudes'
const { initialise, addhabitudes} = useHabitudeStore()
import { onMounted } from "vue";
onMounted(async () => {
    await initialise()
})


const habitudesData = ref({
    nom_habitude : "",
    description : "",
    frequence : "",
    heure_execution: "",
    status : false
})

const insertHabitude = async () =>{
    await addhabitudes(habitudesData.value)
    console.log(habitudes)
}
function closeButton(){
console.log("ok")   
 router.replace("/dahbord")   }
</script>

<style scoped>
.habitForm__content {
    display: flex;
    /* background-color: rgba(0, 0, 0, 0.809); */
    justify-content: center;
    align-items: center;
}

.habit_formBox {
    /* display: none; */
    width: 320px;
    background-color: white;
    box-shadow: rgba(0, 0, 0, 0.08) 0px 4px 12px;
}

.habit_formBox {
    padding: 15px;
}

.habit_form_title {
    padding: 15px;
    display: flex;
    justify-content: space-between;
}

.close {
    cursor: pointer;
}

.input_field {
    margin: 15px;
}

.input_field input {
    padding: 8px 25px;
    margin-top: 10px;
    width: 100%;
    outline: none;
}

.input_field select {
    padding: 8px 25px;
    margin-top: 10px;
    width: 100%;

}

#submit {
    border: none;
    padding: 15px;
    background-color: var(--bleu-side);
    color: var(--white);
    font-weight: bold;
    cursor: pointer;
}
</style>