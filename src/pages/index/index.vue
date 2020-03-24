<template>
    <div>
        <p>
            <router-link to="/index/bobbing">光滑的上下运动</router-link>
        </p>
        <p>
            <router-link to="/index/wavel">线性垂直运动</router-link>
        </p>
        <p>
            <router-link to="/index/pulse">脉冲动画</router-link>
        </p>
        <p>
            <router-link to="/index/random">两个角的波</router-link>
        </p>
        <p>
            <router-link to="/index/wave2">绘制正弦波</router-link>
        </p>
    </div>
</template>

<script>
	export default {
		name: "index",
		created() {
		},
		methods: {

		}
	};
</script>

<style scoped>
</style>
