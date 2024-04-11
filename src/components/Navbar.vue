<template>
    <nav>
        <router-link to="/" id="logo_url">
            <img :src="logo" :alt="alt" id="logo">
        </router-link>
        <div class="links">
            <router-link to="/">Home</router-link>
            <router-link to="/pedidos">Pedidos</router-link>
        </div>
    </nav>
</template>

<script>
export default {
    name: "Navbar",

    props: ["logo", "alt"]
}
</script>

<style scoped>   
    nav {
        background-color: #E4E2DD;
        font-size: 20px;
        display: flex;
        justify-content: flex-end;
        align-items: center;
        padding: 30px;
        max-height: 20vh;
    }

    #logo_url {
        margin: auto;
        margin-left: 0;
    }

    nav #logo {
        height: 60px;
    }

    nav a {
        color: #000;
        text-decoration: none;
        margin: 12px;
        transition: .5s;
        text-transform: uppercase;
    }

    nav a:hover {
        color: #B82E29;
    }

    @media (max-width: 425px) {
        nav {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        margin: 0;
        padding: 20px;
        max-height: 30vh;
        }

        .links {
            width: 100%;
            display: flex;
            justify-content: space-around;
            background-color: #F0D3AD;
        }

        #logo_url {
        margin: 0;
        }

        nav #logo {
        height: 90px;
    }
    }
</style>