<template>
    <footer>
        <p class="direitos">Copyright&copy; 2024 
            <a href="https://carolgonzaga.github.io/projeto-linkme/">
                <strong>Carol Gonzaga</strong>
            </a>
        </p>
    </footer>
</template>

<script>
export default {
    name: 'Footer'
}
</script>

<style scoped>
    footer {
        background-color: #E4E2DD;
        color: #000;
        font-size: 12px;
        display: flex;
        justify-content: center;
        align-items: center;
        padding: 20px;
        max-height: 10vh;
        text-align: center;
    }

    a {
        color: #B82E29;
        text-decoration: none;
    }
</style>