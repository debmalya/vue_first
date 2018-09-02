<template>
    
</template>

<script>
export default {
  name: "Match",
  props: {
    lastUpdated: String,
    homeTeam: String,
    awayTeam: String,
    score: {
        winner: String,
                duration: String,
                fullTime: {
                    homeTeam: Number,
                    awayTeam: Number
                },
                halfTime: {
                    homeTeam: Number,
                    awayTeam: Number
                },
                extraTime: {
                    homeTeam: Number,
                    awayTeam: Number
                },
                penalties: {
                    homeTeam: Number,
                    awayTeam: Number
                }
    }
  }
};
</script>

<style>
</style>
