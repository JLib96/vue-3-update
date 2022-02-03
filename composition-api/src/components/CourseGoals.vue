<template>
  <div>
    <goals-list :goals="filteredGoals"></goals-list>
    <add-goal @add-goal="addGoal"></add-goal>
  </div>
</template>

<script>
import GoalsList from "./GoalsList.vue";
import AddGoal from "./AddGoal.vue";
import{ref,computed} from "vue"

export default {
  components: {
    GoalsList,
    AddGoal,
  },
  setup (props) {
    const goals = ref([]); //DATA 

    const filteredGoals = computed (function(){//COMPUTED
      return goals.value.filter(
        (goal) => !goal.text.includes("Angular") && !goal.text.includes("React")
      );
    });

      function addGoal(text){//METHODS
        const newGoal = {
          id: new Date().toISOString(),
          text: text,
        };
        goals.value.push(newGoal);
      }

    return{//ritorna tutto quello che deve essere disponibile nel template
      filteredGoals,//infatti se cerchi filteredGoals, lo trovi nel template
      addGoal,
    }
  }
  // data() {
  //   return {
  //     goals: [],
  //   };
  // },
  // computed: {
  //   filteredGoals() {
  //     return this.goals.filter(
  //       (goal) => !goal.text.includes("Angular") && !goal.text.includes("React")
  //     );
  //   },
  // },
  // methods: {
  //   addGoal(text) {
  //     const newGoal = {
  //       id: new Date().toISOString(),
  //       text: text,
  //     };
  //     this.goals.push(newGoal);
  //   },
  // },
};
</script>