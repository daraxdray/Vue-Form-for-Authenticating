<template>
        <div id="register" class="navtab-content">
                <form @submit="onSubmit">
                                                    
           <!-- Form Control -->
<div class="control">
            <label class="auth-label">Full Name*</label>
                  <input :style="styles.nameStyles" type="text" @keyup="validateForm('name')" v-model="user.name"  class="input" placeholder="Enter full name">
</div>
                        <!-- Form Control -->
                        <div class="control">
                            <label class="auth-label">Email*</label>
                            <input :style="styles.emailStyles" type="email" @keyup="validateForm('email')" v-model="user.email" class="input" placeholder="Enter email">
                        </div>
                        <!-- Form Control -->
                        <div class="control">
                            <label class="auth-label">Phone*</label>
                            <input :style="styles.phoneStyles" @keyup="validateForm('phone')" type="text" v-model="user.phone" class="input" placeholder="Enter phone" required>
                        </div>
                        <!-- Form Control -->
    <div class="control">
        <label class="auth-label">Password*</label>
        <div class="pw1">
            <input :style="styles.pwStyles" type="password" v-model="pa1" @change="validateForm('password')" class="input " placeholder="Enter password">
            <input :style="styles.pwStyles" type="password" v-model="pa2" @keyup="validateForm('password')" class="input" placeholder="Confirm Password">
        </div>
        <div :class="{ alert: isalert, alertDanger: isalert}">{{message }}</div>
    </div>
    
    <div class="control">
        <label class="auth-label">Sex*</label>
        <div class="pas">
            <input type="radio" v-model="user.sex" name="gender" class="pas1 radio" value="male"> Male<br>
            <input type="radio" v-model="user.sex" name="gender" class="pas1 radio"  value="female"> Female<br>
            
        </div>
    </div>

                                                    <!-- Form Control -->
                                                    <!-- <div class="control">
                                                        <label class="checkbox-wrap is-small">
                                                            <input id="house" type="checkbox" class="d-checkbox" checked>
                                                            <span></span>
                                                            <small>Remember me?</small>
                                                        </label>
                                                    </div> -->
                                                    <!-- Form Submit -->
                                                    <div class="button-wrapper">
                                                        <button :disabled = "disable" type="submit" class="button feather-button is-small primary-button upper-button raised">
                                                            <span>sign-up</span>
                                                        </button>
                                                        <!-- <a class="forgotten">Forgot Password ?</a> -->
                                                    </div>
                                                </form>
                                            </div>

</template>

<script>
import { mapActions } from 'vuex';

export default {
    name: "register",

    data(){
        return{
            user: {
                name:"",
                email:"",
                phone:"",
                password:"",
                sex:""
            },
            message:'',
            pa1:'',
            pa2:'',
            isDisabled: true,
            isalert:false,
            validBorder: '1px solid green',
            validColor: 'green',
            invalidBorder:'1px solid red',
            styles: {
                nameStyles:{
                    border:'',
                    borderColor:''
                },
                emailStyles:{
                    border:'',
                    borderColor:''
                },
                pwStyles:{
                    border:'',
                    borderColor:''
                },
                phoneStyles:{
                    border:'',
                    borderColor:''
                }
            },
            disable: 'true',
            evalid:null,
            phvalid:null,
            pwvalid:null,
            nvalid:null

        };
    }, 

    methods:{
        ...mapActions(['registerUser']),
        
        onSubmit(e){
            e.preventDefault();
            // console.log(this.user);
            this.registerUser(this.user);
        },
matchPassword: function(){
	
	},
 
validateForm: function(type){

    
    if(type == 'email'){
        var e = this.user.email;
         this.evalid = /^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(e)
    if(this.evalid)
        {
                this.styles.emailStyles.borderColor = this.validColor;
                this.styles.emailStyles.border = this.validBorder;
        }
        else{
                this.styles.emailStyles.borderColor = '';
                this.styles.emailStyles.border = '';
               this.evalid = false;
        }
}
else if(type == 'name'){
      var e = this.user.name;
         this.nvalid = /^[a-zA-Z0-9_ ]*$/.test(e)
    if(this.nvalid)
        {
                this.styles.nameStyles.borderColor = this.validColor;
                this.styles.nameStyles.border = this.validBorder;
        }
        else{
                this.styles.nameStyles.borderColor = '';
                this.styles.nameStyles.border = '';
               this.nvalid = false;
        }

}
else if(type=='password'){
	var cpass = this.pa2;
		var pass = this.pa1;
		if(cpass != pass){
            this.styles.pwStyles.border= this.invalidBorder;
		}
        else{
           this.styles.pwStyles.borderColor = this.validColor;
            this.styles.pwStyles.border = this.validBorder;
            this.pwvalid = true;
		}
}
else if(type == 'phone'){
   this.phvalid = /^[\+]?[(]?[0-9]{3}[)]?[-\s\.]?[0-9]{3}[-\s\.]?[0-9]{4,6}$/im.test(this.user.phone);
   if(this.phvalid){
        this.styles.phoneStyles.borderColor = this.validColor;
                this.styles.phoneStyles.border = this.validBorder;
                
   }
   else{
                this.styles.phoneStyles.borderColor = '';
                this.styles.phoneStyles.border ='';
                this.phvalid = false;
   }
}


if(this.phvalid && this.evalid && this.pwvalid && this.nvalid){
this.disable = false;
}else{
    this.disable = true;
}

}}

}



    
    
</script>



<style scoped>
    .pas{
        display: flex;
    }

    .pas1{
        flex: 6;
        border-radius: 0px !important ;
    }
    .pas2{
        flex:6;
        border-radius: 0px !important ;
    }
</style>