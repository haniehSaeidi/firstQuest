<template>
    <div>
        <div class="flex mb-4">
            <div class="w-1/2 h-12 p-3">
                <div class="itinerariesCard">

                </div>
            </div>
            <div class="w-1/2 h-12 p-3">
                <img src="/images/map.png" alt="">
            </div>
        </div>
    </div>
   
</template>
<script>
export default {
    data(){
        return {
            slug:''
        }
    },
    methods: {
        async getCityResult() {
        const url = 'itineraries/?cities=tehran&skip=0&top=5'
        // var qureies={
        //     cities:this.slug,
        //     skip:0,top:5
        // }
        const ip = await this.$axios.$get(url
        // {params:{
        //     cities:[`${this.slug}`],
        //     skip:0,
        //     top:5
        // }}
        )
        .then(res=>{
            console.log(res)
        })
        .catch(err=>err) 
        console.log(ip,'ip')
        },
        
    },
    mounted(){
        var slug = this.$route.params.slug
        this.slug = slug
        this.getCityResult()
    }
}
</script>

<style scoped>

    .itinerariesCard {
        border-radius: 10px;
        border: solid 1px #eaf0f4;
        background-color: var(--white);
        width: 100%;
    }

</style>