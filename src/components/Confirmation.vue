<template>
  <div class="confirmation">
      <div class="confirmation__card">
          <img src="../assets/images/fsi_logo.jpg" alt="FSI Logo" class="confirmation__image">
          <div class="confirmation__details">
              <h3 class="confirmation__details--title">Please Confirm Details Below</h3>
              <p class="confirmation__details--p">Sign up to insure</p>
              <span class="confirmation__details--span">Awesome! We'll need some details from you to get started</span>
              <div class="confirmation__input">
                <input type="text" placeholder="First Name" class="confirmation__details--input">
                <input type="text" placeholder="Last Name" class="confirmation__details--input">
                <input type="text" placeholder="Email Address" class="confirmation__details--input">
                <input type="text" placeholder="Phone Number" class="confirmation__details--input">
              </div>
              <div class="confirmation__btn">
                <button @click="backToReset" class="confirmation__details--btn btn-white">Back</button>
                <button class="confirmation__details--btn">Next</button>
              </div>
          </div>
      </div>
  </div>
</template>

<script>
export default {
    name: 'Confirmation',
    methods: {
        backToReset() {
            return this.$router.push('/signup');
        }
    }
}
</script>

<style lang="scss">
.confirmation {

    &__card {
        height: 55rem;
        width: 90%;
        border-radius: 2rem;
        box-shadow: 0 1.5rem 4rem rgba($color-black, .15);
        position: absolute;
        left: 7rem;
    }

    &__input {
        display: grid;
        grid-template-columns: repeat(2, 40rem);
        grid-gap: 2rem;
    }

    &__btn {
        display: grid;
        grid-template-columns: repeat(2, 15rem);
        grid-gap: 5rem;

        .btn-white {
            background-color: $color-white;
            color: $color-primary;
            border: 1px solid $color-primary;

            &:hover {
                color: $color-white;
            }
        }
    }

    &__image {
        margin-top: 1rem;
        max-width: 20%;
    }

    &__details {
        margin-left: 30rem;
        margin-top: -15rem;

        &--title {
            padding-bottom: 4rem;
            line-height: 1.3;
            color: $color-black;
            font-size: 4rem;
            font-weight: 700;
        }

        &--p {
            font-size: 2rem;
        }

        &--span {
            font-size: 1.5rem;
        }

        &--input {
            display: block;
            padding: 2rem 10rem;
            margin-top: 2rem;
            background:rgba(69, 143, 246, 0.1);
            border-radius: 1rem;
            border: none;

            &:focus {
                outline: none;
            }

            &::placeholder {
                padding-right: 2rem;
            }
        }

        &--btn {
            border: none;
            margin-top: 4rem;
            border-radius: 10rem;
            background-color: $color-primary;
            padding: 1rem 5rem;
            color: $color-white;
            font-size: 1.8rem;

            &:hover {
                cursor: pointer;
                background-color: lighten($color-primary, 5%);
            }
        }
    }
}

@media only screen 
  and (min-device-width: 320px) 
  and (max-device-width: 667px) 
  and (-webkit-min-device-pixel-ratio: 2) {
      .confirmation {

        &__card {
            height: auto;
            width: 100%;
            border-radius: 2rem;
            box-shadow: 0 1.5rem 4rem rgba($color-black, .15);
            position: absolute;
            left: 0;
        }

        &__image {
            margin-top: 1rem;
            max-width: 20%;
            box-shadow: 0px 4px 10px -6px rgba(120, 120, 118, 0.25);
        }

        &__details {
            margin-left: 3rem;
            margin-top: 0;

            &--title {
                padding-bottom: 4rem;
                line-height: 1.3;
                color: $color-black;
                font-size: 4rem;
                font-weight: 700;
            }
        }

        &__input {
            display: grid;
            grid-template-columns: repeat(1, 31.5rem);
            grid-gap: 2rem;
        }

        &__btn {
            display: grid;
            grid-template-columns: repeat(2, 15rem);
            grid-gap: 2rem;
        }
      }
  }
</style>