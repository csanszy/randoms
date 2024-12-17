<template> 
<!-- <RouterLink to="/">
  <Button icon="pi pi-arrow-left" class="custom-button" aria-label="Back" />
</RouterLink> -->
    <div class="containerr p-5 flex justify-center items-center w-full h-full text-pink-400">
    
      <div class="login-box flex flex-col w-full h-[45%] xl:w-[20%] lg:w-[30%] md:w-[40%] sm:w-[50%]
       bg-black rounded-lg">
        <h2 class="text-center text-2xl font-bold p-6">Bejelentkezés</h2>
        <form @submit.prevent="handleLogin" class="flex flex-col gap-1  text-center">
          <div class="user-box">
            <label class="" >Felhasználónév</label><br>
            <input type="text" v-model="email" required="" class="bg-blue-500">
          </div>
          <div class="line1"></div>
          <div class="user-box">
            <label>Jelszó</label><br>
            <input type="password" v-model="password" required="" class="bg-blue-500">
          </div>
          <div class="line"></div>
          <a
            href="#"
            :class="['submit', { disabled: !isFormValid }]"
            :disabled="!isFormValid"
            @click="isFormValid && handleLogin"
          >
            Belépés
          </a>
          <router-link to="/listing">
            <div class="folytdiv"><a class="folyt pt-4">Folytatás bejelentkezés nélkül</a></div>
          </router-link>
        </form>
      </div>
    </div>
    </template>
    
    
    <script>
  export default {
    data() {
      return {
        email: '',
        password: ''
      };
    },
    computed: {
      isFormValid() {
        return this.email.length > 0 && this.password.length > 0;
      }
    },
    methods: {
      handleLogin() {
        console.log('Email:', this.email);
        console.log('Jelszó:', this.password);
      }
    }
  };
    </script>
    
    <style scoped>
  
  
    /* html {
      height: 100%;
    }
    .custom-button {
    font-size: 18px; 
    padding: 20px 20px; 
    width: auto; 
    height: 50px; 
    cursor: pointer;
  }
  
    .containerr {
    height: 100dvh;
    background: url('../../../imgs/night.jpg') no-repeat center center;
    background-size: cover;
    mix-blend-mode: var(--_mesh-gradient-blend-mode);
    }

    @media (max-width: 768px) {
    .containerr {
        background: url('/courseController/SZF1_13_Frontend_CourseController/CourseController/src/Views/LandingPage/képek/nightWest.jpg') no-repeat center center;
        background-size: cover;
        }
    }

    @media (max-width: 480px) {
    .containerr {
        background-position: top;
        background-size: contain;
        }
    } */
/* 
    @media (max-width: 400px) {
      .login-box{
      width: 300px;
      height: 340px;
      }
      .login-box .user-box input{
        width: 250px;
      }
      .login-box h2 {
        font-size: 8px;
      }
      .line{
        width: 250px;
      }
      .line1{
        width: 250px;

      }
    }
  
  
    .login-box {
      position: absolute;
      top: 50%;
      left: 50%;
      width: 380px;
      padding: 40px;
      height: 420px;
      transform: translate(-50%, -50%);
      background: rgba(0, 0, 0, 0.726);
      box-sizing: border-box;
      box-shadow: 0 13px 25px 3px rgba(0, 0, 0, 0.822),
                  inset 0 2px 15px #000000;
      border-radius: 23px;
      backdrop-filter: blur(15px);
    }
    
    .login-box h2 {
      margin: 10px 0 35px;
      padding: 0;
      color: #fff;
      text-align: center;
      font-size: 40px;
    }
    
    .login-box .user-box {
      position: relative;
      top: 15px;
    }
    
    .login-box .user-box input {
      width: 300px;
      padding: 10px 0;
      font-size: 16px;
      color: #ffffff;       
      margin-bottom: 30px;
      border: none;
      outline: none;
      background: transparent;
    }
   */
    /* .line{
      width: 300px;
      margin-bottom: 30px;
      border: none;
      border-bottom: 2px solid #CD90FB;
      outline: none;
      position: absolute;
      bottom: 116px;
      box-shadow: 0px 4px 20px 2px #000000;
    }
  
    .line1{
      width: 300px;      
      margin-bottom: 30px;
      border: none;
      border-bottom: 2px solid #CD90FB;
      outline: none;
      position: absolute;
      bottom: 190px;
      box-shadow: 0px 4px 20px 2px #000000;
    }
  
    .login-box .user-box label {
      position: absolute;
      top:0;
      left: 0;
      padding: 10px 5px;
      font-size: 16px;
      color: #785AEE;
      pointer-events: none;
      transition: .3s;
    }
    
    .login-box .user-box input:focus ~ label,
    .login-box .user-box input:valid ~ label {
      top: -20px;
      left: 0;
      color: #785AEE;
      font-size: 12px;
      padding: 10px 0px;
    }
    
    .login-box form {
      display: flex;
      flex-direction: column;
      align-items: center;
  }
  
    .submit {
      background-color: #CD90FB;
      color: rgb(0, 0, 0);
      border: none;
      cursor: pointer;
      transition: background-color 0.4s;
    }
  
    .submit.disabled {
      cursor: not-allowed;
      opacity: 0;
      pointer-events: none; 
      transition: none; 
    }
  
    .submit.disabled span {
      display: none;
    }
  
    .login-box form .submit {
      position: relative;
      padding: 12px 28px;
      font-size: 16px;
      text-decoration: none;
      transition: .5s;
      letter-spacing: 3px;
      font-weight: bolder;
      border-radius: 10px;
      border: 1px solid rgba(0, 0, 0, 0.26);
      box-shadow: 0px 3px 10px 0px #000000bb;
      margin-bottom: 10px;
      display: inline-block;
      text-align: center;
      width: 140px;
      animation: shadows 1.7s infinite;
    }
    
    @keyframes shadows {
    0% {
      box-shadow: 0px 0px 50px 1px #CD90FB;
    }
    50% {
      box-shadow: 0px 0px 40px 1px rgba(94, 94, 94, 0.5);
    }
    100% {
      box-shadow: 0px 0px 50px 1px #CD90FB;
    }
  }
  
    .login-box form .submit:hover {
      width: 300px;
      background: #CD90FB;
      color: black;
      border: 1px solid rgba(255, 255, 255, 0);
      animation:  none;
      box-shadow: 0 0 5px #CD90FB,
                  0 0 25px #CD90FB,
                  0 0 50px #CD90FB,
                  0 0 100px #CD90FB;
    }
    
    .folytdiv {
      position: absolute;
      bottom: 25px; 
      left: 50%;
      transform: translateX(-50%); 
  }
  
  .folyt {
    text-decoration:underline;
      font-size: 13px;
      color: #fff;
      display: block;
      text-align: center; 
  }
   */
    </style>
  