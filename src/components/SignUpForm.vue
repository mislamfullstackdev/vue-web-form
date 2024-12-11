<template>
  <form @submit.prevent="handleSubmit">
    <label for="">Email</label>
    <input type="email" required v-model="email"/>

    <label for="">Password</label>
    <input type="password" required v-model="password"/>
    <div v-if="passwordError" class="passError">{{ passwordError }}</div>

    <label for="">Role</label>
    <select v-model="role">
        <option value="developer">Developer</option>
        <option value="analist">Analist</option>
        <option value="manager">Manager</option>
        <option value="designer">Programmer</option>
        <option value="programmer">Programmer</option>
    </select>
    <div class="terms">
        <input type="checkbox" required v-model="terms"/>
        <label for="">Agree our terms and conditions</label>
    </div>
    <div class="skills">
        <label for="">Skills</label>
        <input type="text" v-model="tempSkill" @keyup="addSkill"/>
    </div>
    <div class="skills-set" v-for="skill in skills" :key="skill">
        <span @click="deleteSkill(skill)">{{ skill }}</span>
    </div>
    <div class="submit">
        <button>Create an Account</button>
    </div>
  </form>
  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Password: {{ role }}</p>
  <p>Terms: {{ terms }}</p>
</template>

<script>
export default {
    data(){
        return{
            email: '',
            password: '',
            role: 'designer',
            terms: false,
            tempSkill: '',
            skills: [],
            passwordError: '',

        }
    },
    methods:{
        addSkill(e){
            if(e.key === ',' && this.tempSkill.trim()){
                const cleanSkill = ',' && this.tempSkill.replace(/,$/, '').trim();
                if(!this.skills.includes(cleanSkill)){
                    this.skills.push(cleanSkill)
                }
                this.tempSkill = ''
            }
        },
        deleteSkill(skill){
            this.skills = this.skills.filter((item) => {
                return skill != item
            }
        )
        },
        handleSubmit(){
            //validate password
            this.passwordError = this.password.length > 5 ? 
                '' : 'Password must be alteast 5 characters long'
            if(!this.passwordError){
                console.log("Email : ", this.email)
                console.log("Password : ", this.password)
                console.log("Role : ", this.role)
                console.log("Terms : ", this.terms)
                console.log("Skills", this.skills)
            }
        }
    }
}
</script>

<style>
    form {
        max-width: 420px;
        margin: 30px auto;
        background: white;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
    label {
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6rem;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
    input, select {
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555;
    }
    input[type="checkbox"]{
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position: relative;
        top: 2px;
    }
    .skills-set{
        display: inline-block;
        margin: 20px 10px 0 0;
        padding: 6px 12px;
        background: #eee;
        border-radius: 20px;
        font-size: 12px;
        letter-spacing: 1px;
        font-weight: bold;
        color: #777;
        cursor: pointer;
    }
    button{
        background: #0b6dff;
        border: 0;
        padding: 10px 20px;
        margin-top: 20px;
        color: white;
        border-radius: 20px;
    }
    .submit{
        text-align: center;
    }
    .passError{
        color: red;
        margin-top:10px ;
        font-size: 0.8rem;
        font-weight: bold;
    }
</style>