<template>
  <div class="form-container">
    <div class="d-lg-none arrow-responsive">
      <a href="#" @click="toggleForm">
        <img src="../assets/ArrowCircle.png">
      </a>
    </div>

    <div class="d-lg-block d-none arrow">
      <a href="#" @click="toggleForm">
        <img src="../assets/ArrowCircle.png">
      </a>
    </div>

    <div class="plant-image-container">
      <img src="../assets/image.png" class="plant-image">
    </div>

    <h2 class="py-4">Login</h2>

    <div class="pb-2">
      <p class="mb-0">Welcome back!</p>
      <p>Please login to continue</p>
    </div>

    <form @submit.prevent="handleLogin">
      <div class="input-group">
        <input type="email" v-model="email" placeholder="Email Address" required>
        <img src="../assets/email.png" class="input-icon">
      </div>
      <div class="input-group">
        <input :type="passwordFieldType" v-model="password" placeholder="Password" required>
        <img src="../assets/padlock.png" class="input-icon">
        <img src="../assets/Password.png" class="toggle-password-icon" @click="togglePasswordVisibility">
      </div>
      <button type="submit" class="btn">Login</button>
    </form>
    
    <a class="link-password pt-4 pb-5" href="#" @click="sendPasswordResetEmail">Forgot Password</a>

    <p class="text-center social-text pt-5">Or Continue with Social Accounts</p>

    <div class="text-center pb-5 pt-3">
      <a class="social-btn" href="https://www.google.com.br/" target="_block">
        <img src="../assets/Google.png">
      </a>
      <a class="social-btn" href="https://www.facebook.com/" target="_block">
        <img src="../assets/Facebook.png">
      </a>
      <a class="social-btn" href="https://www.apple.com/br/" target="_block">
        <img src="../assets/Apple.png">
      </a>
      <a class="social-btn" href="https://x.com/" target="_block">
        <img src="../assets/Twitter.png">
      </a>
    </div>

    <div class="text">
      Don't have an account? <a class="text-link" href="#" @click="toggleForm">Create Now</a>
    </div>

    <p v-if="loginMessage" :class="{'login-success': loginSuccess, 'login-error': !loginSuccess}" class="login-message">{{ loginMessage }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      showPassword: false,
      loginMessage: '',
      loginSuccess: false
    };
  },
  computed: {
    passwordFieldType() {
      return this.showPassword ? 'text' : 'password';
    }
  },
  methods: {
    handleLogin() {
      const isValidEmail = this.validateEmail(this.email);
      const isValidPassword = this.validatePassword(this.password);
      
      if (isValidEmail && isValidPassword) {
        this.loginSuccess = true;
        this.loginMessage = "Login successful!";
      } else {
        this.loginSuccess = false;
        if (!isValidEmail && !isValidPassword) {
          this.loginMessage = "Both email and password are invalid.";
        } else if (!isValidEmail) {
          this.loginMessage = "Email is invalid.";
        } else {
          this.loginMessage = "Password is not strong enough.";
        }
      }
    },
    toggleForm() {
      this.$emit('toggleForm');
    },
    togglePasswordVisibility() {
      this.showPassword = !this.showPassword;
    },
    sendPasswordResetEmail() {
      alert("A password reset email has been sent to your email address.");
    },
    validateEmail(email) {
      const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      return re.test(email);
    },
    validatePassword(password) {
      const re = /^(?=.*[a-zA-Z])(?=.*\d)(?=.*[@$!%*?&]).{8,}$/;
      return re.test(password);
    }
  }
};
</script>

<style scoped>
.form-container {
  margin: auto;
  padding: 30px;
  background: #ffffff;
  border-radius: 10px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.arrow {
  padding-top: 40px;
}

.arrow-responsive {
  padding-top: 180px;
}

.plant-image-container {
  position: relative;
  text-align: center;
}

.plant-image {
  position: absolute;
  top: -110px;
  right: -30px;
  width: 200px;
  height: auto;
}

h2 {
  font-size: 24px;
  font-weight: 400;
  line-height: 28.08px;
  text-align: left;
  color: #20130B;
}

p {
  font-size: 14px;
  font-weight: 400;
  line-height: 19.32px;
  text-align: left;
  color: #8B8B8B;
}

.input-group {
  margin-bottom: 15px;
  position: relative;
}

.input-group input {
  width: 100%;
  padding: 20px 20px 20px 50px;
  border: 1px solid #ddd;
  border-radius: 5px !important;
  position: relative;
}

.input-icon {
  position: absolute;
  left: 20px;
  top: 50%;
  transform: translateY(-50%);
}

.toggle-password-icon {
  position: absolute;
  right: 20px;
  top: 50%;
  transform: translateY(-50%);
  cursor: pointer;
}

.btn {
  width: 100%;
  padding: 20px;
  background: #BC8363;
  color: white;
  border: none;
  border-radius: 8px;
  margin-top: 10px;
}

.btn:hover {
  background: #BC8363;
  color: white;
}

.link-password {
  font-size: 13px;
  font-weight: 400;
  line-height: 15.21px;
  color: #BC8363;
  text-decoration: none;
  display: block;
  text-align: center;
}

.social-text {
  font-size: 13px;
  font-weight: 400;
  line-height: 15.21px;
  color: #8B8B8B;
}

.social-btn {
  background: #FFFFFF;
  border: none;
  border-radius: 8px;
  padding: 20px 20px;
  cursor: pointer;
  margin-right: 15px;
  box-shadow: 10px 10px 10px 0px #0000000A;
}

.text {
  font-size: 13px;
  font-weight: 400;
  line-height: 15.21px;
  text-align: center;
  color: #8B8B8B;
}

.text-link {
  color: #BC8363;
  text-decoration: none;
}

.login-message {
  font-size: 16px;
  font-weight: 500;
  line-height: 19px;
  text-align: center;
  margin-top: 20px;
}

.login-success {
  color: green;
}

.login-error {
  color: red;
}
</style>
