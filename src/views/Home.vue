<template>
  <div class="container home">
    <ul v-for="character in characters" :key="character.id" class="list">
      <li><strong>{{ character.name }}</strong> ({{ character.actor}})</li>
    </ul>
  </div>
</template>

<script>
import gql from "graphql-tag";

export default {
    name: "MainComp",
    apollo: {
        // nome della query definita nello schema che sta sul server
        characters: gql`
            query {
                characters {
                    id
                    name
                    actor
                    actorLink
                    imgLink
                }
            }
        `,
    },
};
// esempi di query e mutation
// query characterById{
//   character(where: {id: "ckfpi1wcvhnwv0a352nsve6r4"}){
//     name
//     actor
//   }
// }
// mutation addNewCharacter{
//   createCharacter(data:{
//                    name: "Uhura"
//                    actor: "Zoe Saldana"
//                              })
//                 {
//                   name
//                 }
// }
</script>

<style scoped>
.list {
    padding-left: 0;
    list-style-type: none;
}
</style>

