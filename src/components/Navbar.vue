<template>
    <div class="nav">
        <RouterLink to="/" id="logoUrl">
            <img :src="logo" :alt="alt" id="logo" />
        </RouterLink>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/pedidos">Pedidos</RouterLink>

    </div>

</template>

<script>
export default {
    name: "Navbar",
    props: ["logo", "alt"],
}
</script>

<style scoped>
.nav {
    background-color: #222;
    border-bottom: 4px solid #111;
    padding: 15px 50px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    position:sticky;
    width: 100%;
    top:0;
}

#logoUrl {
    margin: auto;
    margin-left: 0;
}

#logo {
    width: 40px;
    height: 40px;
}

.nav a {
    color: #fcba03;
    text-decoration: none;
    margin: 12px;
    transition: .5s;
}

.nav a:hover {
    color: white;

}
</style>

