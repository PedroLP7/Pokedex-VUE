<template >
    <div>

        <h4 class="text-center">SEARCH BY POKEDEX NUMBER</h4>

    <select name="idSearch" id="idSearch" class="form-select" v-model="selectedId" @change="filterById()">    
        <option value="1-151">All</option>    
        
        <option value="1-20">1-20</option>
        <option value="21-40">21-40</option>
        <option value="41-60">41-60</option>
        <option value="61-80">61-80</option>
        <option value="81-100">81-100</option>
        <option value="101-120">101-120</option>
        <option value="121-140">121-140</option>
        <option value="141-151">141-151</option>




    </select>
        
    </div>
</template>
<script>
export default {
    name: 'Selector',
    data() {
        return {
            selectedId:  "1-151",
           
            
        }
    },
    methods: {
        filterById() {
            this.showNumbers = true;
            // console.log(this.selectedId)
            this.$emit('filter-by-id', this.selectedId)
        },
       
    },
    
}
</script>
<style >
#idSearch{
    margin: 0 auto;
    display: block;
    width: 30%;
}
    
</style>