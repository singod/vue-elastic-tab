<style scoped>
        * {
                color: #fff;
				font-size: 14px;
        }
		a {
			text-decoration: none;
		}
		ol {
			 margin: 0;
			 padding: 0;
			 list-style-type: none;
			 
		}
        .active {
                background: #2d8cf0;
        }

        .olX {
                list-style: none;
                white-space: nowrap;
                display: table;
        }

        .liX {
                padding: 6px;
                display: inline-block;
        }
		.liY {
				padding: 6px;
			
		}
</style>
<template>
	<div>
		<div :style="navstyle" :id="GNavId" >
			<ol :class="{olX: GDirection == 'x'}">
				<li v-for="(item,index) in navname" :key="index" :class="{active : (index == ins) && (navlink == null), liX : GDirection == 'x',liY : GDirection == 'y'}">
					<a v-if="navlink != null && navlink.length == navname.length" :href="navlink[index]">
					{{ item }}
					</a>
					<span v-else @click="active(index)">{{ item }}</span>
				</li>
			</ol>
		</div>
	</div>
</template>
<script>
        export default {
                name: 'vue-g-huitan',
                props: {
                        GDirection: {
                                type: String,
                                default: "y"
                        },
                        GNavName: {
                                type: [Array, Object]
                        },
                        GNavLink: {
                                type: [Array, Object]
                        },
                        GNavId: {
                                type: String,
                                default: "g_navid"
                        },
                        GMaxWithY: {
                                type: Number
                        },
                        GBg: {
                                type: String,
                                default: "#ececec"
                        }
                },
                data() {
                        return {
                                ins: 0,
                                navstyle: '',
                                navstyleY: {
                                        width: '100%',
                                        maxWidth: this.GMaxWithY + 'px',
                                        height: '100vh',
                                        background: this.GBg,
                                        textAlign: 'center',
                                        overflow: 'hidden'



                                },
                                navstyleX: {
                                        background: this.GBg,
                                        width: '100%',
                                        overflow: 'hidden',

                                },
                                navId: this.GNavId,
                                navname: '',
                                navlink: '',
                                startX: 0, // 开始的偏移
                                translateX: 0, // 保存的偏移
                                startY: 0, // 开始的偏移
                                translateY: 0, // 保存的偏移
                                startFinger: 0, // 手指坐标
                                maxWidth: '',
                                lastTime: 0, // 按下的时间
                                slide: '',
                                nav: ''

                        }
                },
                beforeCreate() {

                },
                methods: {
                        active(num) {
                                this.ins = num;
								
                        },
                        touchstartX(e) {
                                e.stopPropagation();
                                this.startFinger = e.changedTouches[0].clientX;
                                this.nav.style.WebkitTransition = this.nav.style.transition = '';
                                this.startX = this.translateX;
                                this.lastTime = Date.now();

                                this.maxWidth = this.nav.offsetWidth - this.slide.clientWidth;
                        },
                        touchmoveX(e) {
                                e.stopPropagation();
                                var nowFinger = e.changedTouches[0].clientX,
                                        distance = nowFinger - this.startFinger;
                                this.translateX = distance + this.startX;
                                // 弹性
                                if (this.translateX > 0) { //拖动系数. 拉力的感觉
                                        this.translateX *= 0.4;
                                } else if (this.translateX < -this.maxWidth) { //最后.
                                        this.translateX = distance * 0.4 + this.startX;
                                }
                                this.shiftX(this.translateX);
                        },
                        touchendX(e) {
                                /*
                                	 惯性原理:
                                	 产生的速度 = 移动距离 / 移动时间
                                	 距离 = 松开的坐标 - 上次的坐标  (距离差)
                                	 时间 = 松开的时间 - 按下的时间  (时间差)
                                */
                                var nowFinger = e.changedTouches[0].clientX,
                                        distance = nowFinger - this.startFinger, //距离差
                                        timeDis = Date.now() - this.lastTime, //时间差
                                        speed = (distance / timeDis) * 100;
                                // console.log(speed); //很小 *倍数
                                // 惯性
                                this.translateX += speed;

                                // 边界 ,弹回去
                                if (this.translateX > 0) {
                                        this.translateX = 0;
                                } else if (this.translateX < -this.maxWidth) {
                                        this.translateX = -this.maxWidth;
                                }
                                // 添加贝塞尔曲线
                                this.nav.style.WebkitTransition = this.nav.style.transition = 'transform 500ms cubic-bezier(0.1, 0.57, 0.1, 1)';
                                this.shiftX(this.translateX);
                        },
                        bindEvent(el) {
                                this.slide = el;
                                this.nav = el.firstElementChild || el.firstChild;

                                el.addEventListener('touchstart', this.touchstartX, false)
                                el.addEventListener('touchmove', this.touchmoveX, false)
                                el.addEventListener('touchend', this.touchendX, false)
                        },
                        shiftX(value) {
                                this.nav.style.WebkitTransform = this.nav.style.transform = 'translateX(' + value + 'px)';
                        },
                        touchstartY(e) {
                                e.stopPropagation();
                                this.startFinger = e.changedTouches[0].clientY;
                                this.nav.style.WebkitTransition = this.nav.style.transition = '';
                                this.startY = this.translateY;
                                this.lastTime = Date.now();

                                this.maxWidth = this.nav.offsetHeight - this.slide.clientHeight;
                        },
                        touchmoveY(e) {
                                e.stopPropagation();
                                var nowFinger = e.changedTouches[0].clientY,
                                        distance = nowFinger - this.startFinger;
                                this.translateY = distance + this.startY;
                                // 弹性
                                if (this.translateY > 0) { //拖动系数. 拉力的感觉
                                        this.translateY *= 0.4;
                                } else if (this.translateY < -this.maxWidth) { //最后.
                                        this.translateY = distance * 0.4 + this.startY;
                                }
                                this.shiftY(this.translateY);
                        },
                        touchendY(e) {
                                /*
                                	 惯性原理:
                                	 产生的速度 = 移动距离 / 移动时间
                                	 距离 = 松开的坐标 - 上次的坐标  (距离差)
                                	 时间 = 松开的时间 - 按下的时间  (时间差)
                                */
                                var nowFinger = e.changedTouches[0].clientY,
                                        distance = nowFinger - this.startFinger, //距离差
                                        timeDis = Date.now() - this.lastTime, //时间差
                                        speed = (distance / timeDis) * 100;
                                // console.log(speed); //很小 *倍数
                                // 惯性
                                this.translateY += speed;

                                // 边界 ,弹回去
                                if (this.translateY > 0) {
                                        this.translateY = 0;
                                } else if (this.translateY < -this.maxWidth) {
                                        this.translateY = -this.maxWidth;
                                }
                                // 添加贝塞尔曲线
                                this.nav.style.WebkitTransition = this.nav.style.transition = 'transform 500ms cubic-bezier(0.1, 0.57, 0.1, 1)';
                                this.shiftY(this.translateY);
                        },
                        bindEventY(el) {
                                this.slide = el;
                                this.nav = el.firstElementChild || el.firstChild;

                                el.addEventListener('touchstart', this.touchstartY, false)
                                el.addEventListener('touchmove', this.touchmoveY, false)
                                el.addEventListener('touchend', this.touchendY, false)
                        },
                        shiftY(value) {
                                this.nav.style.WebkitTransform = this.nav.style.transform = 'translateY(' + value + 'px)';
                        }


                },
                mounted() {
                        if (this.GDirection == '') {
                                alert("请设置导航方向")
                        } else if (this.GDirection == 'x') {
                                this.navname = this.GNavName;
                                this.navlink = this.GNavLink;

                                this.navstyle = this.navstyleX;
                                var navid = '#' + this.navId;
                                var ctx = document.querySelector(navid);
                                this.bindEvent(ctx);

                        } else if (this.GDirection == 'y') {
                                this.navname = this.GNavName;
                                this.navlink = this.GNavLink;

                                this.navstyle = this.navstyleY;
                                var navid = '#' + this.navId;
                                var ctx = document.querySelector(navid);
                                this.bindEventY(ctx);

                        }


                }

        }
</script>
