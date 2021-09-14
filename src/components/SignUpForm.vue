<template>
  <form  @submit.prevent="handelSubmit">
    <label>Email address</label>
    <input type="email" required v-model="email">

    <label>password</label>
    <input type="password" required v-model="password">
    <div v-if="passwordError" class="error"> {{passwordError }} </div>

    <label>Role :</label>
    <select v-model="role">
        <option value="developer">web developer</option>
        <option value="designer">web designer</option>
    
    </select>

    <div class="terms">
    <input type="checkbox" required v-model="terms">
    <label>Accept terms and conditions</label>
  </div>

  <label>Skills</label>
  <input type="text" @keyup.alt="addSkill" v-model="tempSkills" >
  
  <div v-for="skill in skills" :key="skill" class="pill">
    <span @click="deleteSkill(skill)"> {{ skill }}</span> 
  </div>

  <div class="submit">
    <button>Create an account</button>
  
  </div>

  </form>


  <p> email : {{ this.email }}</p>
  <p> password : {{ this.password }}</p>
  <p>role :{{this.role }} </p>
  <p>terms aacepted:{{this.terms}}</p>

</template>

<script>
export default {
    data(){
        return{
            email : '',
            password : '',
            role : 'designer',
            terms: false,
            tempSkills :'',
            skills : [],
            passwordError:'',
        
        }
    },

    methods:{
        addSkill(event){
            if(event.key === ',' && this.tempSkills){
                if(!this.skills.includes(this.tempSkills)){
                    this.skills.push(this.tempSkills)
                    
                }
                this.tempSkills = ''
                
            }
        },
        deleteSkill(skill){
            this.skills = this.skills.filter((item) => { 
                return skill !== item // if equal return false and remove 
            })

        },
        handelSubmit(){
            this.passwordError = this.password.length >5 ?
             '' : 'password must be at least 6 chars long'

             if(!this.passwordError){
                console.log('email ' + this.email);
                console.log('pass ' + this.password);
                console.log('role ' + this.role);
                console.log('skills ' + this.skills);
                console.log('terms accepted ' + this.terms);

             }
        }
    }

}
</script>

<style>

form{
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}

label{
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: .6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;

}

input , select{
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
    margin: 0 10px 0 0 ;
    position: relative;
    top:px;

}

.pill{
    display: inline-block;
    margin :20px 10px 0 0 ;
    padding : 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color:#777;
    cursor: pointer;


}

button{
    margin-top :20px ;
    padding : 10px 20px;
    background: #0b6dff;
    border: 0px;
    color:white;    
    border-radius: 20px;


}

.submit {
text-align: center;

}

.error{
    color :#ff0062;
    margin-top: 10px;
    font-size: .8em;
    font-weight: bold;


}
</style>