<template>
    <div id="paramdetails">
        The paremeter value that was passed to me is: {{ $route.params.id }}        
    </div>
</template>

<script>
    export default {
    name: 'Paramdetails'
    }
</script>