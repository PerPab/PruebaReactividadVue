
<template>
    <div class="container-fluid d-flex flex-row m-0 p-0 principal">

        <div class="frame ">
            <div>
                <h5 class="text-center mt-1">Character Generator</h5>
                <hr/>

                <div class="container-fluid d-flex flex-column align-items-center form-group">
                    <label><h5 class="text-center">Name</h5></label>
                    <input class="form-control text-center" v-model="character.characterName" >

                    <label><h5 class="text-center mt-2">Gender</h5></label>
                    <select class="form-control" v-model="character.charcaterGender">
                    <option class="text-center">Male</option>
                    <option class="text-center">Female</option>
                    </select> 

                    <label><h5 class="text-center mt-2">Race</h5></label>
                    <select class="form-control" v-model="character.characterRace">
                    <option class="text-center">Human</option>
                    <option class="text-center">Elf</option>
                    <option class="text-center">Orc</option>
                    
                    </select> 

                    <label><h5 class="text-center mt-2">Class</h5></label>
                    <select class="form-control" v-model="character.characterClass">
                    <option class="text-center">Warrior</option>
                    <option class="text-center">Mage</option>
                    <option class="text-center">Rogue</option>
                    <option class="text-center">Archer</option>                  
                    </select>
                    
                    <div class="check">
                        <label><h5 class="text-center mt-1">Abilities</h5></label>
                        <hr/>
                            <div class="form-check p-0 m-0">
                                <input v-model="character.characterAbilities" class="form-check-input" type="checkbox" value="One Handed" id="abilities1">
                                <label class="form-check-label" for="abilities1">
                                One Handed
                                </label> 
                            </div>

                            <div class="form-check p-0 m-0">
                                <input v-model="character.characterAbilities" class="form-check-input" type="checkbox" value="two Handed" id="abilities2">
                                <label class="form-check-label" for="abilities2">
                                two Handed
                                </label> 
                            </div>

                            <div class="form-check p-0 m-0">
                                <input v-model="character.characterAbilities" class="form-check-input" type="checkbox" value="Light Armor" id="abilities3">
                                <label class="form-check-label" for="abilities3">
                                Light Armor
                                </label> 
                            </div>

                            <div class="form-check p-0 m-0">
                                <input v-model="character.characterAbilities" class="form-check-input" type="checkbox" value="Heavy Armor" id="abilities4">
                                <label class="form-check-label" for="abilities4">
                                Heavy Armor
                                </label> 
                            </div>

                            <div class="form-check p-0 m-0">
                                <input v-model="character.characterAbilities" class="form-check-input" type="checkbox" value="Block" id="abilities5">
                                <label class="form-check-label" for="abilities5">
                                Block
                                </label> 
                            </div>

                            <div class="form-check p-0 m-0">
                                <input v-model="character.characterAbilities" class="form-check-input" type="checkbox" value="Sneak" id="abilities6">
                                <label class="form-check-label" for="abilities6">
                                Sneak
                                </label> 
                            </div>
                    </div>
                    <div class="abilities-list p-2">
                        <label><h5 class="text-center mt-1">Selected Abilities</h5></label>
                        <ul class="list-group list-group-vertical wrap text-center">
                            <li v-for="ability in character.characterAbilities" v-bind:key="ability">{{ ability }}</li>
                        </ul>
                    </div>                       
                </div> 
            </div>
        </div>
        <div class="frame">
            <h5 class="text-center mt-1">Character Resume</h5>
                <hr/>
                <div class="resume d-flex justify-content-center">
                    <div class="card">
                        <div class="d-flex m-2">
                            <img v-bind:src="profileImg()" class="img-responsive" alt="...">

                        </div>
                    <hr/>
                    <div class="card-body p-0">
                    <h5 class="card-title text-center fw-bold">{{character.characterName}}</h5>
                    <h6 class="text-center">{{ character.charcaterGender }}</h6>
                    <h6 class="text-center">{{ character.characterRace }}</h6>
                    <h6 class="text-center">{{ character.characterClass }}</h6>                                                                                      
                    </div>
                    <div v-if="character.characterClass!=''&&character.characterName!=''" class="container-fluid d-flex justify-content-center">
                        <button v-on:click="addCharacter()" class="btn btn-success">Add to group</button>
                    </div> 
                    <div v-else class="container-fluid d-flex justify-content-center">
                        
                    </div> 
                </div>
            </div>

                <hr/>
                <h5 class="text-center">Group</h5>
                <div class="group m-4">
                    <table class="table text-center">
                     <thead>
                     <tr>
      
                       <th scope="col"><h5>Name</h5></th>
                       <th scope="col"><h5>Race</h5></th>
                       <th scope="col"><h5>Class</h5></th>
                       </tr>
                      </thead>
                     <tbody>
                       <tr v-for="item in characterGroup" v-bind:key="item.characterName">      
                        <td><h6 class="table-item">{{ item.charName }}</h6></td>
                        <td><h6 class="table-item">{{item.charRace}}</h6></td>
                        <td><h6 class="table-item">{{ item.charClass }}</h6></td>
                      </tr>
    
                        </tbody>
                        </table>
        </div>         
        </div>
    </div>
</template>

<script setup>
import {ref} from 'vue';

let character = ref({
    characterName: '',
    charcaterGender:'',
    characterRace: '',
    characterClass:'',
    characterAbilities:[]

})

let characterGroup =ref([])

//let img="/img/logo.png"

function profileImg(){
    if(character.value.charcaterGender=='Male' && character.value.characterRace =='Human'){
        return "/img/humanmale.png"
    }
    if(character.value.charcaterGender=='Female' && character.value.characterRace =='Human'){
        return "/img/humanfemale.png"
    }
    if(character.value.charcaterGender=='Male' && character.value.characterRace =='Orc'){
        return "/img/orcmale.png"
    }
    if(character.value.charcaterGender=='Female' && character.value.characterRace =='Orc'){
        return "/img/orcfemale.png"
    }
    if(character.value.charcaterGender=='Male' && character.value.characterRace =='Elf'){
        return "/img/elfmale.png"
    }if(character.value.charcaterGender=='Female' && character.value.characterRace =='Elf'){
        return "/img/elffemale.png"
    }
    else{
        return "/img/logo.png"

    }

    }





function addCharacter(){
    characterGroup.value.push({
        charName:character.value.characterName ,
        charGender: character.value.charcaterGender,
        charRace:character.value.characterRace ,
        charClass:character.value.characterClass ,
        charAbilities:character.value.characterAbilities=[]
    })
    character.value.characterAbilities=[]
    character.value.characterName=''
    character.value.characterClass=''
    character.value.characterRace=''
    character.value.charcaterGender=''
}

</script>

<style scoped>

ul{
list-style-type:none;
}

.table-item{
    color: darkblue;
}

.abilities-list{
    width: 60%;
    height: 100%;
    background-color: aliceblue;
}

.card{
    width: 15rem;
    margin: 0 auto;
    min-height: 310px;
}
.img-responsive{
    width: 50%;
    margin: 0 auto;
}

.form-check-input{
    width: 20px;
    height: 20px;
    margin: 5px; 
}
.form-check-label{
    width: fit-content;
}

.check{
    background-color: aliceblue;
    width: 60%;
    margin-top: 1rem;
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    flex-wrap: wrap;
    padding: 10px;  
}

label{
    width: 100%;
}
input, select{
    width: 60%;
    border-radius: 0;
      
}
.principal{
    background: rgb(245,249,191);
    background: radial-gradient(circle, rgba(245,249,191,1) 0%, rgba(207,210,156,1) 89%);
}
.frame{
    width: 100%;
    height: 100vh;
    
    
}
@media (max-width: 640px) {
    .frame{
        
        width:100%;
        height: fit-content;        
    }
    .principal{
        display: flex;
        flex-wrap: wrap;
        flex-direction: column;
        justify-content: center;
    }
    .check, .abilities-list{
        width: 80%;
    }
}

</style>