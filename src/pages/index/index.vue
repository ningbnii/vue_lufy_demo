<template>
    <div>
        <p>
            <router-link to="/bobbing">光滑的上下运动</router-link>
        </p>
        <p>
            <router-link to="/wavel">线性垂直运动</router-link>
        </p>
        <p>
            <router-link to="/pulse">脉冲动画</router-link>
        </p>
        <p>
            <router-link to="/random">两个角的波</router-link>
        </p>
        <p>
            <router-link to="/wave2">绘制正弦波</router-link>
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
