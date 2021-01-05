<template>
  <div class="signup">
      <div class="signup__card">
          <router-link to="/">
          <img src="../assets/images/fsi_logo.jpg" alt="FSI Logo" class="signup__image">
          </router-link>
          <div class="signup__details">
              <h3 class="signup__details--title">Find The Right Health Insurance <br>
                    Plan For You
              </h3>
              <p class="signup__details--p">Sign up to insure</p>
              <span class="signup__details--span">Awesome! We'll need some details from you to get started</span>
              <input type="text" v-model="bvn" placeholder="Enter BVN" class="signup__details--input">
              <button @click="verifyBVN" class="signup__details--btn">Next</button>
          </div>
      </div>
  </div>
</template>

<script>
import aesjs from 'aes-js'
export default {
    name: 'SignUp',
    data () {
        return {
           bvn: ''
        }
    },
    methods: {
        verifyBVN() {
            let keys = JSON.parse(sessionStorage.getItem('credentials'));
            let aesKey = aesjs.utils.hex.toBytes(keys['aes_key']);
            let ivKey = aesjs.utils.hex.toBytes(keys['ivkey']);
            let bvnBytes = aesjs.utils.utf8.toBytes(this.bvn);
            let aesCbc = new aesjs.ModeOfOperation.cbc(aesKey, ivKey);
            let encryptedBVN = aesCbc.encrypt(bvnBytes);
            let encryptedBVNHex = aesjs.utils.hex.fromBytes(encryptedBVN);
            console.log('encrypted', encryptedBVNHex);
            return this.$router.push('/confirmation');
        }
    }
}
</script>

<style lang="scss">
.signup {

    &__card {
        height: 52rem;
        width: 80%;
        border-radius: 2rem;
        box-shadow: 0 1.5rem 4rem rgba($color-black, .15);
        position: absolute;
        left: 13.3rem;
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
            margin-top: 4rem;
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
      .signup {

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
                line-height: 1.3;
                color: $color-black;
                font-size: 4rem;
                font-weight: 700;
            }
            br {
                display: none;
            }
        }
      }
  }
</style>