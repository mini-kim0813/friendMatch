<template>
	<div class="login">
		<h1>SemiColon</h1>
		<br />
		<form class="LoginForm">
			<p>
				<label for="memberIdInput">ID</label>&nbsp;
				<input type="text" id="memberIdInput" class="input_text" ref="memberIdInput" v-model.trim="memberId"
					placeholder="아이디를 입력하세요." />
			</p>
			<p>
				<label for="memberPasswordInput">PW</label>
				<input type="password" id="memberPasswordInput" class="input_text" ref="memberPasswordInput"
					v-model.trim="memberPassword" placeholder="비밀번호를 입력하세요." />
			</p>
			<div class="login_etc">
				<div class="checkbox">
					<input type="checkbox" name="SaveSession" id="SaveSession"> 정보를 저장할까요?
				</div>
				<br />
				<div class="forgot_account">
					<a @click="fnFindId"> 아이디</a> 혹은 <a @click="fnFindPw"> 비밀번호</a>를 잊으셨나요?
				</div>
			</div>
			<br />
			<div class="SubmitAccount">
				<span>만약 계정이 없다면, <router-link to="/register">회원가입</router-link>을 먼저 진행해주세요!</span>
			</div>
			<p class="buttons">
				<button @click.prevent="doLogin" type="button" class="btn btn-primary" data-bs-toggle="modal"
					data-bs-target="#PwNull">로그인</button>
				<button @click.prevent="doCancel" type="button" class="btn btn-primary" data-bs-toggle="modal"
					data-bs-target="#PwNull">취소</button>
			</p>
		</form>
	</div>

</template>

<script>
import userList from "@/assets/UserData.json";

export default {
	name: 'LoginForm',
	data : function() {
		return {
			memberId : '',
			memberPassword : '',
			errorMessage : '',
			data : userList,
		};
	},
	methods : {
		doLogin() {
			if (document.getElementById("memberIdInput").value == "") {
				alert("아이디를 입력해주세요!");
				document.getElementById("memberIdInput").focus();
      } else if (document.getElementById("memberPasswordInput").value == "") {
				alert("비밀번호를 입력해주세요!");
				document.getElementById("memberPasswordInput").focus();
            
			} else if (document.getElementById("memberIdInput").value == userList.id && document.getElementById("memberPasswordInput").value== userList.password) {
				alert(this.memberId + "님 환영합니다.");
				this.$router.push('/login/success/:memberId');
			
			} else {
				alert("없는 계정입니다.")
			}
		},
		doCancel() {
			document.getElementById("memberIdInput").value = null;
			document.getElementById("memberPasswordInput").value = null;
			document.getElementById("memberIdInput").focus();
		},
		fnFindId() {
			// this.$refs.memberIdInput && this.memberPasswordInput.trim();
			this.$router.push('/findId')
		},
		fnFindPw() {
			// this.$refs.memberIdInput && this.memberPasswordInput.trim();
			this.$router.push('/findPw')
		},
	},
	mounted() {
		document.getElementById("memberIdInput").focus();
	}
};
</script>

<style scoped>
/* Google Fonts Import */
@import url('https://fonts.googleapis.com/css2?family=Black+Han+Sans&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Jua&display=swap');

/* Import End */

body {
	margin: 0;
}

div {
	box-sizing: border-box;
}

.black-bg {
	width: 100%;
	height: 100%;
	background: rgba(0, 0, 0, 0.5);
	position: fixed;
	padding: 20px;
}

.white-bg {
	width: 100%;
	background: white;
	border-radius: 8px;
	padding: 20px;
}

div .login { background-color: white; }

.login { 
	width: 800px; 
	margin: 20px auto;
}
.login h1 { 
	text-align: center; 
	font-family: 'Black Han Sans', sans-serif; 
}
.LoginForm { 
	margin: auto; 
	text-align: left;
}
.LoginForm p > label { 
	display: inline-block; 
	font-size: 24px; 
	padding-right: 16px;
	align-items: center; 
	font-family: 'Black Han Sans', sans-serif; 
}
.LoginForm p > .input_text { 
	width: 100%;
	height: 50px;
	text-align: center;
	font-family: 'Jua', sans-serif;
	border-radius: 30px;
	margin-top: 10px;
	outline: none;
	font-size: 22px;
	align-items: center;
}

.LoginForm p > .input_text:focus { 
	font-size: 180%;
}

.buttons { 
	position:relative; 
	height:32px; 
	margin-top:20px; 
	text-align: center;
}
/* .buttons > .button { overflow:visible; cursor:pointer; min-width:125px; height:32px; margin:0 2px; padding:0 15px; line-height:32px; font-size:14px; border:1px solid #dfdfdf; background:#fff; border-radius:10px;  margin-top: 20px; width: 80%; font-weight: bold; } */
.buttons > .button { 
	overflow: visible; 
	cursor: pointer; 
	min-width:125px; 
	height: 40px;
	margin:0 2px; 
	padding:0 15px; 
	line-height: 32px; 
	font-size: 1.2em;
	border: 0;
	/* border:1px solid #dfdfdf;  */
	background: #D3D3D3; 
	border-radius: 40px;  
	margin-top: 20px;
	margin-left: 10px;
	width: 80%; 
	font-weight: bold; 
	outline: none;
}

.buttons > .button.blue { 
	color:#fff; 
	border-color:#0099d2 !important; 
	background:#0099d2 !important; 
	margin-top: 20px; 
	align-items: center;
	width: 80%; 
	font-weight: bold;
	border-radius: 40px;
}

.login_etc {
  padding: 12px;
  width: 100%;
  font-size: 16px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-weight: bold;
  text-align: center;
  margin-left: 10px;
}

.login_etc > .forgot_account > a {
	text-decoration: underline;
}

div .SubmitAccount {
	padding: 12px;
	width: 100%;
	font-size: 16px;
	display: flex;
	justify-content: space-between;
	align-items: center;
	font-weight: bold;
	text-align: center;
	margin-left: 10px;
}
</style>
