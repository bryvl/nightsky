<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import {ref, onMounted, computed, watch} from 'vue'
// this characters 
// const characters = ref([])
const charTraits = ref([])


const charRoles = ref([
  {
    roleName: "Colossus",
    roleThumb: "/src/assets/NS_Colossus_Thumb.PNG",
    roleColor: "#ff978d",
    roleDescription: "test"
  },
  {
    roleName: "Valkyrie",
    roleThumb: "/src/assets/NS_Valkyrie_Thumb.PNG",
    roleColor: "#ffc478",
    roleDescription: "testing"
  },
  {
    roleName: "Weaver",
    roleThumb: "/src/assets/NS_Weaver_Thumb.PNG",
    roleColor: "#eaabff",
    roleDescription: "also test"
  },
  {
    roleName: "Dancer",
    roleThumb: "/src/assets/NS_Dancer_Thumb.PNG",
    roleColor: "#b6f4ff",
    roleDescription: "also testing"
  },
  {
    roleName: "Vocalist",
    roleThumb: "/src/assets/NS_Vocalist_Thumb.PNG",
    roleColor: "#5bfd85",
    roleDescription: "Loooving Youuuu"
  }
])
const charOrigins = ref([
  {
    originNumber: 1,
    originRace: 'human',
    originDescription: 'A standard human from Earth' 
  },
  {
    originNumber: 2,
    originRace: 'avianni',
    originDescription: 'Evolvants from the other side of the Milky Way, dwellers of the sky'
  },
  {
    originNumber: 3,
    originRace: 'praenobis',
    originDescription: 'A promethean civilization pre-dating all known races'
  },
  {
    originNumber: 4,
    originRace: 'simulacra',
    originDescription: 'Shades of the conscious beings they once were, these cyber-humans have augmented themselves out of a soul'
  }
])
const active_el = 0
const char_name  = ref('')
const char_gender  = ref(null)
const char_race  = ref(null)
const char_class = ref(null)


const addTrait = () => {
  if (input_content.value.trim() === '' || input_category.value === null) {
    return
  }
  charTraits.value.push({
    charName: char_name.value,
    charGender: char_gender.value
  })
  input_content.value = ''
  input_category.value = null
}
  const activeOrigin = ref(null);

let showDescription = (origin) => {

  let originParagraph = document.getElementById("origin-description")
  originParagraph.textContent = ""

  let btnContainer = document.getElementById("origin-btn-container")
  let btns = document.getElementsByClassName("origin-button")

  let originText = document.createTextNode(origin.originDescription)
  originParagraph.appendChild(originText)
}

</script>

<template>
  <div class="container-fluid game-bg">
    <div class="row">
      <div class="col-xs-12">
        <h1>Night Sky</h1>
      </div>
      <div class="col-xs-12">
        <form @submit.prevent="addTrait">
          <h4 class="text-center">Tell us more about yourself, traveler...</h4>
          <div class="row">
            <div class="col-xs-12 creation-section">
              <h3 class="input-title">What is your name?</h3>
              <input type="text" 
              class="form-input"
              v-model="char_name"
              />
            </div>
            <div class="col-xs-12 text-center">
              <h4>What is your gender?</h4>
              <div class="options">
                <label>
                  <input 
                    type="radio"
                    name ="gender"
                    value="Male"
                    v-model="char_gender" />
                  <span class="bubble"></span>
                  <div>Male</div>
                </label>
                <label>
                  <input 
                    type="radio"
                    name ="gender"
                    value="Female"
                    v-model="char_gender" />
                  <span class="bubble"></span>
                  <div>Female</div>
                </label>
                <label>
                  <input 
                    type="radio"
                    name ="gender"
                    value="Nonbinary"
                    v-model="char_gender" />
                  <span class="bubble"></span>
                  <div>Non-binary</div>
                </label>
              </div>
            </div>
            <!-- Next Steps: make classes and race sections -->
            <div class="col-xs-12 creation-section">
              <h3 class="input-title">Choose Your Origin: </h3>
              <div class="row">
                <div class="col-2">
                  <div class="row origin-btn-container">
                    <a 
                      :id="`${origin.originRace}-button`" 
                      class="col-12 role-thumb origin-button"  
                      v-for="origin in charOrigins" 
                      :key="origin"
                      :class="{ 'active' : activeOrigin == origin}"
                      @click="activeOrigin = origin; showDescription(origin)"
                      >
                      {{origin.originRace}}
                    </a>
                  </div>
                </div>
                <div class="col-10">
                  <p id="origin-description"></p>
                </div>
                <div class="col-12 origin-submit-col">
                    <a class="origin-submit" :key="origin">So you are of the ?</a>
                </div>
              </div>
              <label>
                <input 
                  type="text" 
                  class="form-input"
                  v-model="char_race"
                  />
              </label>
            </div>
            <div class="col-12 creation-section class-section">
              <h3 class="input-title">Choose Your Class: </h3>
              <div class="row">
                <div class="col-6 col-lg-2 role-card" v-for="role in charRoles">
                  <div class="row">
                    <div class="col-12 role-thumb">
                      <div class="role-thumb-wrapper">
                        <img :src="role.roleThumb">
                      </div>
                      <h4 class="text-center" :class="`${role.roleName.toLowerCase()}-theme`">{{role.roleName}}</h4>
                    </div>
                  </div>
                  <div :class="`${role.roleName.toLowerCase()}-theme-bg`"></div>
                </div>
              </div>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
