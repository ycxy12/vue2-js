<!--
 * @Author: yc
 * @Date: 2024-11-23 11:45:16
 * @LastEditors: yc
 * @LastEditTime: 2024-11-24 15:40:10
 * @Description: 头部
-->
<template>
	<el-header height="64px">
		<h3>开源QB</h3>
		<el-dropdown @command="handleCommand">
			<span class="el-dropdown-link">
				<i class="el-icon-user-solid"></i>
				{{ getUserInfo.userName }}
				<i class="el-icon-arrow-down el-icon--right"></i>
			</span>
			<el-dropdown-menu slot="dropdown">
				<el-dropdown-item command="logout">退出登录</el-dropdown-item>
			</el-dropdown-menu>
		</el-dropdown>
	</el-header>
</template>

<script>
import { mapGetters, mapMutations } from "vuex"
export default {
	data() {
		return {}
	},
	computed: {
		...mapGetters(["getUserInfo"]),
	},
	methods: {
		...mapMutations(["clearState"]),
		handleCommand(command) {
			switch (command) {
				case "logout":
					this.logout()
					break
				default:
			}
		},
		logout() {
			this.$confirm("您是否确认退出登录?", "温馨提示", {
				confirmButtonText: "确定",
				cancelButtonText: "取消",
				type: "warning",
			}).then(() => {
				this.clearState()
				this.$router.replace("/")
				this.$message.success("退出登录成功！")
			})
		},
	},
}
</script>

<style lang="scss" scoped>
.el-header {
	width: 100%;
	display: flex;
	align-items: center;
	justify-content: space-between;
	z-index: 20;
	padding: 0 20px 0;
	color: #fff;
	background-color: #001529;
	box-shadow: 0 1px 4px rgba(0, 21, 41, 0.08);
	.el-dropdown {
		color: #fff;
		cursor: pointer;
		&:hover {
			color: #1890ff;
		}
	}
}
</style>
