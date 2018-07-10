<template>
  <div id="app">		
		<vue-g-huitan
			GDirection="y" 
			:GNavName="li_array" 
			:GNavLink="li_array_link"
			GNavId="tanxinNav"
			
			GBg="#5cadff" 
			
			:GMaxWithY="100" 
			
			:GElastic="150"></vue-g-huitan>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
			li_array: ["前面的","world","love","china","前面的","world","love","china","前面的","world","love","china","前面的","world","love","china","前面的","world","love","china","前面的","world","love","china","前面的","world","love","china","前面的","world","love1","china","前面的2","world2","love2","china2","前面的3","world3","love3","china3","前面的4","world4","love4","china4","前面的5","world6","love","china","前面的","world","love","china","前面的","world","love","china","前面的","world","love","china","前面的","world","love","china","hello","world","love","china"],
			li_array_link: ["/hello123","/world","/love","china","hello","world","love","china","hello","world","love","china","hello","world","love","china","hello","world","love","china","hello","world","love","china","hello","world","love","china","hello","world","love1","china","hello2","world2","love2","china2","hello3","world3","love3","china3","hello4","world4","love4","china4","hello5","world6","love","china","hello","world","love","china","hello","world","love","china","hello","world","love","china","hello","world","love","china","hello","world","love","china"]
				
    }
  }
}
</script>

<style>

</style>
