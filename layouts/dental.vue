<template>
    <v-app class=˜image˜>
        <div>
            <v-content>
                <v-container>
                    <nuxt />
                </v-container>
            </v-content>
        </div>
    </v-app>
</template>

<script>
export default {

}
</script>

<style>
.image {
    position:relative;
    width: 100%;
    height: 100%;
    background-image: linear-gradient(rgba(24, 23, 26, 0.75),
      rgba(24, 23, 26, 0.75)),
      url(~static/login.jpeg);
      background-repeat: no-repeat;
      background-size: cover;

}

.layout {
    height: 55vh;
}
</style>
