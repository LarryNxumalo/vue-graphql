<template>
    <ul>
        <li v-for="(rocket, index) in rockets" :key="index">
            <h2>{{rocket.name}}</h2>
            <h3>{{rocket.description}}</h3>
            <p>${{rocket.cost_per_launch}}</p>
        </li>
    </ul>
</template>

<script>
//GQL Needed to be able to send graphQL query strings properly parsed to graphql servers
import gql from "graphql-tag"

const query = gql`
    query getRockets {
    capsule(id: "") {
        id
    }
    rockets {
        id
        name
        description
        costPerLaunch: cost_per_launch
    }
    }`
//Apollo object that allows us to use the apollo object in our vue-comp
export default {
    apollo: {
        rockets: {
            query
        }
    }
}
</script>