<script > 
export default {
  name: "app",

  data() {
    return {
      newmenu: "",
	  newprepo:"",
	  newpic:null,
      indexEditTodo: null,
      tempNameTodo: "",
      tempStatusTodo: "",
      todoStatus: ["to-do", "on-going", "finished"],
      menus: [ 
      ],
	  prepo:[]
    };
  },
  methods: {
	addMenu() {
      if (this.newmenu.length === 0) return;
      if (this.indexEditTodo === null) {
		this.prepo.push(this.newprepo)
        this.menus.push({
          name: this.newmenu,
		  pic:this.newpic,
		  preson:this.prepo
        });
		
      } else {
        this.menus[this.indexEditTodo].name = this.newmenu;
        this.indexEditTodo = null;
      }
      this.newmenu = "";
	  this.newpic = null
	},
	switchTab (tabName){
	let newTab = tabName;
  let thisPanel = document.querySelector('#'+tabName);
  let oldPanel = '';
	if (tabName == "menu") {
		 oldPanel = document.querySelector('#people');
	}
	else{
		 oldPanel = document.querySelector('#menu');	
	}
	oldPanel.style.display = "none";
	thisPanel.style.display = "block";
	if (oldTab != newTab) {
		document.querySelectorAll('.tabName')[0].classList.toggle('cl-grey');
		document.querySelectorAll('.tabName')[1].classList.toggle('cl-grey');
		document.querySelectorAll('.tabLine')[0].classList.toggle('bg-grey-2');
		document.querySelectorAll('.tabLine')[1].classList.toggle('bg-grey-2');
	}
	oldTab = newTab;
}
}



}
</script>

<template>

<body>
        <main>
                <div class="form">
               
                  <section id="header" class="padding-rm ">
			<theboxes class="bottom spacing-s -clip">
				<box col="4" mob="4"><inner class="">
					<div class="h8">จำนวนคน</div>
					<div class="h4" id="peopleSize_wrap">0</div>
				</inner></box>
				<box col="5" mob="5"><inner class=" ">
					<div class="h8">ราคารวม</div>
					<div class="h4" id="price_wrap">0</div>
				</inner></box>
				<!-- <box col="3" mob="3"><inner class="  t-center">
					<div class="size-s upper b7" id="qr_label">Add PromptPay</div>
					<sp class="s"></sp>
					<img src="assets/qr.png" class="qr" id="qr_pic" v-on:click="addQr()">
					<sp class="s"></sp>
				</inner></box> -->
			</theboxes>
		</section>
		<sp class="px bg-smoke"></sp>
		<section id="tab" class="t-center b7 size-l">
			<theboxes class="top -clip" boxing="2" mob="2">
				<box col=""><inner class="" @click="switchTab('menu')"  >
					<div class="tabName padding cl-lightblue">
						<i class="size-m fas fa-stream"></i>&nbsp;&nbsp;
						<span>รายการ</span>
					</div>
					<sp class="tabLine xs bg-lightblue"></sp>
				</inner></box>
				<box col=""><inner class="" @click="switchTab('people')">
					<div class="tabName padding cl-lightblue cl-grey">
						<i class="size-m fas fa-user-friends"></i>&nbsp;&nbsp;
						<span>คนจ่าย</span>
					</div>
					<sp class="tabLine xs bg-lightblue bg-grey-2"></sp>
				</inner></box>
			</theboxes>
		</section>
		<section id="people">
			<div class="padding-rm">
				<theboxes class="top spacing-l -clip size-m cl-grey">
					<box col="8" mob="8"><inner class="">
						ชื่อคน
					</inner></box>
					<box col="2" mob="2"><inner class="t-right">
						จ่าย
					</inner></box>
					<box col="2" mob="2"><inner class="t-center">
						
					</inner></box>
				</theboxes>
				<theboxes class="middle spacing-l -clip size-l cl-vblack" id="peopleList">
					
				</theboxes>
				<sp class="vl"></sp>
				<form onsubmit="return addPeople(input_peopleName)">
					<theboxes class="top spacing -clip">
						<box col="9" mob="9"><inner class="">
							<input type="text" id="input_peopleName" class="ffont input wide cl-black" placeholder="ระบุชื่อ"  >
						</inner></box>
						<box col="3" mob="3"><inner class="">
							<button class="ffont btn t-center wide b7 bg-lightblue hover-bg-lightblue-6 padding-vs-hzt">
								เพิ่ม
							</button>
						</inner></box>
					</theboxes>
				</form>
				<sp class="vl"></sp>
				<span class="cl-red-8 size-m pointer" v-on:click="clearCache('people')">
					ล้างรายชื่อคนจ่ายทั้งหมด
				</span>
			</div>
		</section>
		<section id="menu">
			<div class="padding-rm">
				<theboxes class="top spacing-l -clip size-m cl-grey">
					<box col="8" mob="8"><inner class="">
						ชื่อรายการ
					</inner></box>
					<box col="2" mob="2"><inner class="t-right">
						ราคา
					</inner></box>
					<box col="2" mob="2"><inner class="t-right">
						คนละ
					</inner></box>
				</theboxes>
				<theboxes class="top spacing-l -clip size-m " v-for="(todo, index) in menus"
      :key="index">
					<box col="8" mob="8"><inner class="">
						{{ todo.name }}
					</inner></box>
					<box col="2" mob="2"><inner class="t-right">
						{{ todo.pic }}
					</inner></box>
					<box col="2" mob="2"><inner class="t-right">
						<!-- {{ todo.preson }} -->
					</inner></box>
				</theboxes>
	
				<sp class="vl"></sp>
				<div >
					<theboxes class="top spacing -clip">
						<box col="5" mob="5" >
             
							<input type="text"  class="ffont input wide cl-black" placeholder="ระบุรายการ" v-model="newmenu" >
							
					
					</box>
					<box col="5" mob="5">
						
							<input type="number"  class="ffont input wide cl-black" placeholder="ระบุราคา" v-model="newpic" >
							
						
					</box>
						<box col="3" mob="3">
							<button type="submit" class="submit-btn px-3 py-2" @click="addMenu()">
        +
      </button>
						</box>
					</theboxes>
					
				</div>
				<sp class="vl"></sp>
				<span class="cl-red-8 size-m pointer" v-on:click="clearCache('menu')">
					ล้างรายการทั้งหมด
				</span>
			</div>
		</section>
		
         
                </div>
               
       
        </main>
       
    </body>

  </template>

<style scoped>
/*=============== GOOGLE FONTS ===============*/
@import url("https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;600&display=swap");
@import url('https://cdn.jsdelivr.net/npm/boxicons@latest/css/boxicons.min.css');
@import url('https://jabont.com/jayss/jayss.css');
/*=============== VARIABLES CSS ===============*/
@font-face {
	font-family: 'Maledpan';
	src: url('maledpan-regular-webfont.woff2') format('woff2');
	font-weight: normal;
	font-style: normal;
}

body{
	background-color: #fdfdfd;
	--mainHeight : unset;
	--mainOverflow : unset;
	--calHeight : 0px;
	--popup_menu_wrap_bg : #fff;
	/*margin-bottom: 56px;*/
	overflow-x:unset;
	-webkit-user-select: none;
	/*-webkit-tap-highlight-color: transparent;*/
	-webkit-touch-callout: none;
}
.can-select{
	-webkit-user-select: text;
	-webkit-tap-highlight-color: auto;
	-webkit-touch-callout: auto;
}
body[popup="1"]{
	--mainHeight : 100%;
	--mainOverflow : hidden;
}
body[cal="1"]{
	--calHeight : 250px;
	--popup_menu_wrap_bg : #fff;
}
.ffont{
	font-family: 'Maledpan' !important;
}

body[popup="1"] .disclaim{
	display: none;
}
main{
	margin:0 auto;
	width: 100%;
	max-width: 420px;
	height: var(--mainHeight);
	overflow: var(--mainOverflow);
}
.btn{
	cursor: pointer;
}
.quick-add{
	display: none;
	position: fixed;
	right: .5em;
	bottom: .5em;
	width: 2em;
	line-height: 2em;
	text-align: center;
	color:white;
	font-size: 1.5em;
}
#people{
	display: none;
}
.popup{
	max-width: 420px;
	margin: auto;
}
body[popup="1"] .popupBg{
	background: #0008;
	width: 100%;
	height: 100%;
	position: fixed;
	top: 0;
	left: 0;
}
.popupWrap{
	display: none;
	position: absolute;
	top: 0;
	width: 100%;
	z-index: 500;
	overflow: auto;
	transition: height .2s;
}
#popup_menu{
	height: calc(100% - var(--calHeight));

}
.popupWrap[show="1"]{
	display: flex !important;
}

#popup_people{
	height: 100%;
}
.popup_menu_wrap{
	background-color: var(--popup_menu_wrap_bg);
}

input[type="text"], input[type="email"], input[type="url"], input[type="password"], input[type="search"], input[type="number"], input[type="tel"], input[type="range"], input[type="date"], input[type="month"], input[type="week"], input[type="time"], input[type="datetime"], input[type="datetime-local"], input[type="color"] {
	border: 0;
	border-bottom: 1px solid #aaa;
	border-radius: 0;
	padding-left: 0em;
	padding-right: 0em;
}
input::placeholder{
	color:#ddd;
}
input:focus::placeholder{
	color: transparent;
}
.people-list-wrap{
	display: flex;
	flex-flow: row wrap;
}
.people-list{
	padding: .5em 1em;
	border-radius: 5px;
	background-color: #eee;
	margin: .1em;
	color: #666;
}

.people-list i::before{
	content: "\f067";
}  

.people-list[pay="1"]{
	background: hsl(var(--hue), 100%, 90%);
	color: hsl(var(--hue), 80%, 40%);
}

.people-list[pay="1"] i::before{
	content: "\f00c";
}

.menu-list i::before{
	content: "\f067";
} 
.menu-list[pay="1"] i::before{
	content: "\f00c";
}  
.menu-list{
	color: #666;
}
.menu-list[pay="1"]{
	color: #03A9F4;
}

.people-list i, .menu-list i {
	width: 1em;
	text-align: center;
}
input#input_menuAmout {
	line-height: 0;
	padding: 0;
}
#calculator {
	transition: height .2s;
	position: fixed;
	height: var(--calHeight);
	width: 100%;
	left:0;
	bottom: 0;
	z-index: 1000;
	background: #0008;
}
#calculator .popup{
	box-shadow: 0px 0px 20px 5px rgba(0,0,0,0.1),0px -1px 1px rgba(0,0,0,0.1)
}
#cal_operator{
	display: flex;
	flex-flow: row wrap;
	text-align: center;
}
#cal_operator div{
	width: 100%;
	background: #0001;
	height: 50px;
	display: flex;
	align-items: center;
	justify-content: center;
}
#cal_operator div#op_equals{
	background: #0002;
}
.calpad{
	height: 50px;
	display: flex;
	align-items: center;
	justify-content: center;
}
#cal_operator div:active, .calpad:active{
	background: #0003 !important;
}

.paid-label{
	font-size: .8rem;
	background: hsl(var(--hue), 100%, 90%);
	color: hsl(var(--hue), 80%, 40%);
	padding: .1em .5em .4em;
	border-radius: 3px;
	font-weight: bold;
	margin-left: 1em;
	display: none;
}
.people-main-list{
	color: hsl(var(--hue), 80%, 40%);
}
.people-main-list[pay="1"] .paid-label{
	display: inline-block;
}
.menu-pay-by .paid-label{
	display: inline-block;
	margin: .1em;
}
.qr{
	max-width: 100%;
	margin: auto;
}
.pointer{
	cursor: pointer;
}
#bill_url{
	width: 100%;
	border-radius: 5px; 
	border: 1px solid #999;
	padding: 0em 3em 0em .7em;
	font-size: .8em;
}
#bill_url_copy{
	position: absolute;
	right: 0;
	top: .1em;
	cursor: pointer;
	line-height: 1.8em;
	width: 2em;
	text-align: center;
	border-left: 1px solid #eee;
}
#bill_url_copy:active{
	transform: scale(.9);
}

</style>
