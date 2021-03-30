.<template>
  <div >      

            <Card style="width: 25em">
                <template #header>
                    
                    <img v-bind:src=" user.picture.large" /> 
                </template>
                <template #title>
                    Ususario random 
                </template>                
                <template #content >
                    <p>{{user.name.first}} {{user.name.last}}</p>
                </template>
                <template #footer>
                    <Button icon="pi pi-check" label="Save" @click="onClick()" />
                    <Button icon="pi pi-times" label="Reroll" class="p-button-secondary" style="margin-left: .5em" @click="reRoll()"/>
                </template>
            </Card>
  </div>
</template>

<script>
import Button from 'primevue/button';
import axios from "axios"
export default {
    name: 'Cartas',
    components:{
        Button
    },
    data(){
        return{
            user:{name:"name",picture:"unknow"}
        }
    },
    methods:{
        onClick(){
            console.log("holis")
            axios.post("http://localhost:1337/user",
            {
                name:this.user.name.first,
                lastname:this.user.name.last,
                image:this.user.picture.large
            })
            .then(resp=>console.log(resp.data))
        } ,
        reRoll(){
            console.log("chau")
            axios.get("https://randomuser.me/api/")
            .then(resp=>{
                console.log(resp.data.results)
                this.user=resp.data.results[0]
            })
        }  
    }

}
</script>

<style scoped>
   div{       
       /* margin-left: 10%; */
       display: flex;
       align-items: center;
       align-content: center;
       margin: 10px;
   }
</style>