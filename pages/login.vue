<script>
  export default {
    data() {
      return {
        formData: {
          fullName: "",
          email: "",
          password: "",
        },
      };
    },
    methods: {
      handleLogin() {
        if (this.formData.fullName && this.formData.email && this.formData.password) {
          this.$router.push('/question'); 
        } else {
          alert("Please fill in all the fields!");
        }
      },
    },
  };
  </script>


<template>
    <section class="bg-[#3F0DC5] h-screen">
      <div class="flex justify-center items-center p-10 py-20">
        <div>
          <img src="/images/fingerprint.png" alt="" class="rounded-[60px] w-[500px] rounded-r-none">
        </div>
        <div class="bg-white rounded-2xl px-[80px] py-[63px] rounded-l-none">
          <div class="flex justify-center">
            <img src="/images/checkbox.png" alt="">
          </div>
          <div>
            <h2 class="text-2xl font-bold text-[#101828] mb-6 items-center flex justify-center">Sign in to Quiz App</h2>
            <p class="text-[#475467] mb-4 flex justify-center text-sm">Kindly fill in the following details to get started</p>
            <form @submit.prevent="handleLogin">
              <div class="mb-4">
                <label class="block text-[#344054] font-medium" for="full-name">Full Name</label>
                <input
                  class="mt-2 p-2 w-[325px] border border-[#D0D5DD] rounded-lg"
                  type="text"
                  id="full-name"
                  v-model="formData.fullName"
                  placeholder="Enter your full name"
                  required
                />
              </div>
              <div class="mb-4">
                <label class="block text-[#344054] font-medium" for="email">Email</label>
                <input
                  class="mt-1 p-2 w-[325px] border border-[#D0D5DD] rounded-lg"
                  type="email"
                  id="email"
                  v-model="formData.email"
                  placeholder="Enter your work email"
                  required
                />
              </div>
              <div class="mb-4">
                <label class="block text-[#344054] font-medium" for="password">Password</label>
                <input
                  class="mt-1 p-2 w-[325px] border border-[#D0D5DD] rounded-lg"
                  type="password"
                  id="password"
                  v-model="formData.password"
                  placeholder="Enter your password"
                  required
                />
              </div>
              <button class="w-full bg-[#3F0DC5] text-white py-2 rounded-lg" type="submit">Sign in</button>
            </form>
          </div>
        </div>
      </div>
    </section>
  </template>
  
  
  
 


    