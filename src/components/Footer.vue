<template>
    <footer class="footer">
        <div class="footer__content">
            <p class="footer__content--text"> &copy; FSI Health LTD 2020. All rights reserved. </p>
        </div>
    </footer>
</template>

<script>
export default {
    name: "Footer"
};
</script>

<style lang="scss">
.footer {

    &__content {
        margin-top: 10rem;
        height: 20rem;
        width: 100%;
        background-color: $color-primary;

        &--text {
            text-align: center;
            font-size: 2rem;
            color: $color-white;
            border-top: 1px solid $color-white;
            padding-top: 8rem;
        }
    }
}
</style>