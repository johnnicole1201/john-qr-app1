<template>
    <div>
        <v-container class="d-flex justify-center align-center" style="height: 100vh;">
        
        <v-card max-width="500" class="pa-7">
             <v-card-title>Login Page</v-card-title>
            <v-card-text>
                
                <v-form>
                    <v-text-field
                    
                    outlined
                    rounded
                    prepend-inner-icon="mdi-email"
                    
                    label="Email"
                    type=" Email"
                    >
                </v-text-field>
                <v-text-field
                outlined
                rounded
                prepend-inner-icon="mdi-lock"
                label="Password"
                type="Password"
                >

                </v-text-field>
                <v-btn rounded color="primary" type="submit" class="mt-4" block>LOGIN</v-btn>
                <div class= " text-center my-5"> OR </div>
                
                <v-btn color="error" @click=" signinWithGoogle()" class="text-capitalize" rounded block>
                <v-icon left>mdi-google </v-icon>Sign in with Google  </v-btn>
                
                </v-form>
            </v-card-text >
            <v-card-text>
                <v-form>
                   
                </v-form>
            </v-card-text>
           
        </v-card>
        </v-container>
    </div>
</template>

<script>

export default {
    methods: {
        signinWithGoogle(){
            this.$auth.loginWith('google')
        }, catch (err) {
      console.error('Google Sign-In failed', err)
    }
    }

    
};


</script>