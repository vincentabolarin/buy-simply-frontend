<script setup>
import { ref } from "vue";

import axios from "axios";

import { useToast } from "vue-toastification";

import apiRoutes from "../utils/config";

const toast = useToast();

const email = ref("");
const password = ref("");

const togglePasswordView = () => {
    let input = document.getElementById("password");
    if (input.type === "password") {
      input.type = "text";
    } else {
      input.type = "password";
    }
  }
  const signIn = async (e) => {
    e.preventDefault();

    try {
      let payload = {
        email: email.value,
        password: password.value
      }

      if (payload.email === "" || payload.password === "") {
        toast.error("You must fill in your email address and password.");
      } else {
        const response = await axios.post(apiRoutes.logIn, payload);
        router.push("/dashboard");
        toast.success("You have successfully signed in.");
        return response;
      }
    } catch (error) {
      toast.error("Error signing in.");
    }
  }
</script>

<template>
  <div class="formContainer">
    <div class="heading">
      <p class="welcome">Welcome</p>
      <p class="enterEmail">Enter your email address and password to access your account.</p>
    </div>

    <form @submit="signIn">
      <div class="email">
        <label for="email">Email Address <span>*</span></label>
        <input type="email" name="email" id="email" placeholder="Enter your email" ref="myEmail" v-model="email">
      </div>

      <div class="password">
        <label for="password">Password <span>*</span></label>

        <div class="passwordInput">
          <input type="password" name="password" id="password" placeholder="Enter your password" ref="myPassword" v-model="password">
          <img src="../assets/eye.svg" alt="Eye Icon" class="eyeIcon" @click="togglePasswordView">
        </div>
        
        <div class="passwordExtras">
          <div class="remember">
            <input type="checkbox" name="remember" id="remember">
            <label for="remember" class="rememberLabel">Remember me</label>
          </div>
          <div class="forgot">Forgot Password?</div>
        </div>
      </div>

      <div class="signIn">
        <input type="submit" value="Sign in">
        <p class="signUp">Don't have an account? <span>Sign up</span></p>
      </div>
    </form>
  </div>
</template>

<style lang="scss" scoped>
  .formContainer {
    padding: var(--padding-6) var(--padding-4);
    display: flex;
    flex-direction: column;
    gap: var(--gap-2);

    .heading {
      text-align: center;

      .welcome {
        margin-bottom: var(--margin-1);
        color: var(--color-primary);
        font-size: var(--font-32);
        font-weight: var(--font-700);
        font-family: 'Lora', sans-serif;
      }
    }

    form {
      display: flex;
      flex-direction: column;
      gap: var(--gap-2);
    }

    .email, .password {
      display: flex;
      flex-direction: column;
      gap: var(--gap-0_5);

      span {
        color: var(--color-red);
      }
    }

    .password {
      .passwordInput {
        position: relative;

        .eyeIcon {
          position: absolute;
          right: 0;
          top: 1px;
          height: 46px;
          border-radius: 0 8px 8px 0;
          cursor: pointer;
        }
      }

      .passwordExtras {
        display: flex;
        justify-content: space-between;

        .remember {
          display: flex;
          align-items: center;
          gap: var(--gap-0_5);

          .rememberLabel {
            font-size: var(--font-14);
            font-weight: var(--font-400);
            color: var(--color-gray-3);
          }
        }

        .forgot {
          font-size: var(--font-14);
          font-weight: var(--font-400);
          color: var(--color-primary);
          cursor: pointer;
        }
      }
    }

    .signIn {
      margin-top: var(--margin-1);

      input {
        background-color: var(--color-primary);
        color: var(--color-white);
        font-size: var(--font-15);
        font-weight: var(--font-700);
        cursor: pointer;
      }

      .signUp {
        font-size: var(--font-14);
        font-weight: var(--font-400);
        color: var(--color-gray-1);
        margin-top: var(--margin-0_5);
        text-align: center;

        span {
          font-size: var(--font-14);
          font-weight: var(--font-600);
          color: var(--color-primary);
          cursor: pointer;
        }
      }
    }
  }

  @media screen and (width < 1024px) {
    .formContainer {
      padding: 0;
      width: 80vw;
    }
  }
</style>