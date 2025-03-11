<template>
    <div style="height: 100vh;">
        <el-container>

            <el-header style="height: 5vh;">
                <el-row style="height: 100%;">
                    <el-col :span="24" style="display: flex; justify-content: center; align-items: center;">
                        <div class="header_title">互联网外包公司名单
                            <a style="display: inline-block;"
                               href="https://github.com/lhsaq2009/Are-You-Waibao/issues" target="_blank">
                                <svg viewBox="-1 -1 18 18" style="height: 100%;">
                                    <path d="M8 0c4.42 0 8 3.58 8 8a8.013 8.013 0 0 1-5.45 7.59c-.4.08-.55-.17-.55-.38 0-.27.01-1.13.01-2.2 0-.75-.25-1.23-.54-1.48 1.78-.2 3.65-.88 3.65-3.95 0-.88-.31-1.59-.82-2.15.08-.2.36-1.02-.08-2.12 0 0-.67-.22-2.2.82-.64-.18-1.32-.27-2-.27-.68 0-1.36.09-2 .27-1.53-1.03-2.2-.82-2.2-.82-.44 1.1-.16 1.92-.08 2.12-.51.56-.82 1.28-.82 2.15 0 3.06 1.86 3.75 3.64 3.95-.23.2-.44.55-.51 1.07-.46.21-1.61.55-2.33-.66-.15-.24-.6-.83-1.23-.82-.67.01-.27.38.01.53.34.19.73.9.82 1.13.16.45.68 1.31 2.69.94 0 .67.01 1.3.01 1.49 0 .21-.15.45-.55.38A7.995 7.995 0 0 1 0 8c0-4.42 3.58-8 8-8Z"></path>
                                </svg>
                            </a>
                        </div>
                    </el-col>
                </el-row>
            </el-header>

            <el-main>

                <!-- 01、表单提交 -->
                <el-row style="margin-bottom: 18px;">
                    <el-col :span="24">
                        <el-card class="box-card">
                            <el-row style="display: flex; justify-content: center; align-items: center;">
                                <el-col :span="getColumnSpan">
                                    <el-form :inline="true" style="padding: 0 12px;
                                             display: flex; justify-content: center; align-items: center;">
                                        <el-form-item label="查询公司" style="flex-grow:0.5; margin-bottom: 0;">
                                            <el-input v-model="searchKeyword" placeholder="请输入公司名称"
                                                      show-word-limit clearable size="default"
                                                      @input="highlightKeywords" @clear="reset"
                                                      style="max-width: 600px;"></el-input>
                                            <span v-if="trimmedSearchKeyword"
                                                  style="position: absolute; right: 30px; font-size: 12px; color: #999; }">
                                                {{ count }}
                                            </span>
                                        </el-form-item>
                                    </el-form>
                                </el-col>
                            </el-row>
                        </el-card>
                    </el-col>
                </el-row>

                <!-- 02、列表展示 -->
                <el-row style="margin-bottom: 18px;">
                    <el-col :span="24">
                        <el-card class="box-card">
                            <blockquote style=" text-align: right; color: #999; margin: 0 0 12px 0; ">
                                <span>
                                    欢迎
                                    <a href="https://github.com/lhsaq2009/Are-You-Waibao/issues" target="_blank">Issues</a>
                                    提交新名单，更新：2024-05-31
                                </span>
                            </blockquote>

                            <div class="content">
                                <section id="main">
                                    <video id="player" src="https://dwz.mk/MVZVjy"
                                           autoplay controls="controls" width="100%" height="400px">
                                    </video>
                                </section>
                            </div>
                            <div v-html="highlightedText" style="font-size: 1em;">
                                <p>神州泰岳（北京神州泰岳软件股份有限公司）、 泽佳科技（北京泽佳科益科技有限公司）、 时空云科技有限公司、 盛唐科技、 致远宣大、 北银金科、 京北方、 中软国际、 矩立信息、 软通动力、 中电金信(原文思海辉)、 亚信科技、 法本信息、 慧博云通、 东软集团、 维恩贝特、 南京迈特望、 南京麦思伦、 麦亚信、 深圳思特顺、 深圳易宝、 神州信息、 彩讯科技、 深圳拓保、 绛门科技、 合肥凯捷、 诚迈科技、 纬创软件、 北京天景隆、 宇信科技、 江苏润和软件、 天津喜鹊共享科技、 南京昊亦源、 深圳大展信息科技、 深圳德科信息技术、 广州凯泽利（部分外包）、 深圳青桐盛夏科技、 武汉软帝联合科技、 深圳智慧盾(华付信息)、 浩鲸科技(阿里外包，根据评论添加)、 中科软(根据评论添加)、 柯莱特、 融航信息、 博彦科技、 新致软件、 安硕信息技术、 上海复深蓝软件股份公司、 长亮科技、 浪潮集团、 人瑞集团、 上海思芮、 上海汉朔信息科技、 汉克时代、 卓望信息、 精锐动力、 众信易成、 上海佩航航空科技、 北方科诚、 广州源创信息、 CDC软件、 NTTDATA、 阿米德、 艾融（上海）、 艾斯克雷、 爱思爱、 安硕信息、 奥博杰天、 百微科技、 佰钧成、 北京百胜扬软件技术有限公司、 北京点点企服、 北京护航、 北京华路时代、 北京华胜天成、 北京尖峰、 北京开运联合、 北京新思软件技术有限公司、 北京云核网络、 北京云核网络股份有限公司、 北京长亮合度信息技术有限公司、 北明软件、 北信源、 编码王、 博朗软件、 博彦科技、 博悦科创、 诚迈科技、 晟峰软件、 创博国际、 大汉软件、 大连华信、 大连斯锐信息技术公司、 大连文思海辉信息技术有限公司、 大宇宙信息、 大展科技、 大展信息科技（深圳）有限公司、 得逸信息、 德科信息、 德科信息（深圳）、 第一线安莱、 顶点软件、 顶尖传承、 鼎捷软件（上海）、 东南融通、 东软集团、 咚瓜科技、 法本信息、 泛亚信息技术、 方天科技、 风云科技、 福瑞博德、 复深蓝软件开发、 富基融通、 富士通信息、 高伟达、 广联达（北京）、 广州赛意信息科技股份有限公司、 广州迅维连锁、 国睿科技、 海隆软件、 海通安恒（广东）、 海万科技、 海云数据、 汉得信息（上海）、 汉克时代（北京）、 杭州端点科技、 杭州颐和、 浩鲸科技、 浩鲸智能、 和仁科技、 恒宝、 恒生电子、 宏智科技、 华道数据处理、 华路时代、 华苏科技、 华拓数码、 华通科技、 汇信金服、 慧博云通（北京）、 健友生化、 江苏红网、 江苏鸿信、 江苏慧世联网络科技、 江苏欧索软件、 江苏天鼎、 绛门科技、 金桥信息（上海）、 金色华勤、 金斯瑞、 金现代、 金证股份、 京北方、 经纬国际、 九城关贸、 九洲财务、 久雅科技、 开运联合、 凯捷咨询(中国)有限公司、 柯莱特、 科大国创软件股份公司、 科蓝软件、 蓝凌软件、 朗新科技、 浪潮、 立思辰科技、 联迪恒星、 联合信息、 联想利泰（北京）、 猎宝网、 凌志软件、 领雁科技（北京）、 绿和生活通、 马衡达信息技术（上海）有限公司、 麦肯锡、 麦思伦、 明略科技、 南京绛门信息科技股份有限公司、 南京迈特望、 南京星空在线、 南京银行消费金融中心、 南京云昇、 南天信息、 南威软件、 诺赛软件、 普联软件、 启明软件、 千方科技、 前海泰坦科技（深圳）有限公司、 全速创想（杭州）、 日电卓越、 软通动力、 瑞祥科技、 瑞友云智科技、 睿信天和、 睿至大数据、 润和、 润杨金融、 赛迪通、 赛科斯、 赛意信息（广州）、 三维天地、 山东北明全程物流、 上海艾融软件股份有限公司、 上海晟欧、 上海海隆、 上海海万信息科技股份有限公司、 上海汉得信息技术股份有限公司、 上海浩方、 上海微创软件、 上海微创软件股份有限公司、 上海易宝软件有限公司、 上海易立德信息技术股份有限公司、 上海彧求信息科技有限公司、 上海中软华腾软件系统有限公司、 上海中信信息发展、 申朴信息、 深圳宝润兴业、 深圳鹏开信息技术有限公司、 深圳市博奥特科技有限公司、 深圳市布雷泽科技有限公司、 深圳市德科信息技术有限公司、 深圳市法本信息技术股份有限公司、 深圳市集益创新信息技术有限公司、 深圳市金卫信、 深圳市先进数通融安信息技术、 深圳市雁联计算系统有限公司、 深圳市易思博软件技术有限公司、 深圳市长亮保泰信息科技有限公司、 深圳市长亮核心科技有限公司、 深圳市长亮科技股份有限公司、 深圳市紫川软件有限公司、 深圳四方精创资讯股份有限公司、 深圳四方精创资讯股份有限公司北京分公司、 深圳索信达数据技术有限公司、 深圳网新新思、 深圳兴融联科技有限公司、 深圳雁联技术、 深圳怡化电脑、 深圳银兴科技开发有限公司、 神州数码、 神州信息、 盛安德、 石化盈科、 时代银通（杭州）、 世纪恒通、 斯凯、 斯特沃克（ThoughtWork）、 四川汉科、 四川准达信息（四川）、 四方精创（深圳）、 索迪斯、 拓保软件、 拓维信息、 泰豪科技股份、 泰豪软件、 特力惠、 天阳科技、 通动力信息、 通邮集团、 同和信息、 万国数据服务、 网新博创、 网新新思（深圳）、 微创软件、 纬创软件、 文思海辉、 乌鸫科技（杭州）、 武大吉奥、 武汉佰钧成技术、 西安华炎信息科技有限公司、 西安炎兴、 先进数通、 小草互联、 新大陆软件、 新聚思、 新宇软件、 新致软件、 信必优、 信雅达、 讯方技术（深圳）、 亚信科技、 亚信联创、 药明康德、 亿达信息（大连）、 亿力吉奥、 屹通信息科技、 易宝软件（深圳）、 易诚互动（北京）、 易立德（上海）、 易联达（北京）、 易思博、 懿华软件、 音泰思、 银丰新融、 印孚瑟斯技术（中国）有限公司、 英极软件开发(大连)、 盈达信息、 赢时胜（北京）、 永新视博、 宇信科技、 宇信易诚、 裕宁科技、 元拓科技、 云和恩墨、 云腾未来（贵州）、 在信汇通、 长亮科技、 浙大网新Insigma（杭州）（请注意，据说已不是外包）、 浙江大华、 浙江希优、 知迪、 智慧盾、 中博研究院、 中诚签、 中电金信/文思海辉(北京）、 中国信息技术、 中和软件、 中恒博瑞、 中科创达软件、 中科软、 中软、 中软国际、 中网在线、 中信网科、 中兴软件、 中讯软件、 中盈蓝海、 紫川软件、 紫金支点、 万氪人力、 如是纵横（大连）科技有限公司、 如是纵横（武汉）科技有限公司</p>
                            </div>
                        </el-card>
                    </el-col>
                </el-row>

                <!-- 回到顶部 -->
                <el-row style="">
                    <el-backtop/>
                </el-row>

            </el-main>

        </el-container>
    </div>

</template>

<script>

import {ElMessage} from "element-plus";

export default {
    data() {
        return {
            count: 0,
            searchKeyword: "",
            originalText: "",
            highlightedText: "",

            screenWidth: window.innerWidth,
            player: null
        };
    },

    methods: {
        reset() {
            this.highlightedText = this.originalText;
            this.count = 0;
        },
        highlightKeywords() {

            if (this.searchKeyword.trim().length === 0) {
                this.reset();
                return;
            }

            this.count = 0;
            // 使用正则表达式进行全局替换，并添加样式
            const regex = new RegExp(this.searchKeyword, 'gi');
            this.highlightedText = this.originalText.replace(regex, match => {
                this.count++;
                return `<span class="yellow">${match}</span>`;
            });
        },

        bindEvents() {
            const player = this.player;
            player.addEventListener('error', this.random);
            player.addEventListener('ended', () => {
                this.random();
            });
        },
        random() {
            const player = this.player;
            player.src = 'http://v.nrzj.vip/video.php?_t=' + Math.random();
            player.play();
        }
    },
    created() {

        // 异步函数，定期更新此文件内容
        fetch('https://raw.githubusercontent.com/lhsaq2009/Are-You-Waibao/master/public/companies.txt')
            .then(response => response.text())
            .then(data => {
                const processedArray = data.split(/[\n,，|\s]+/)
                    .filter(item => item.trim() !== '*')
                    .filter(item => item.trim() !== '')
                    .filter((item, index, array) => array.indexOf(item) === index); // 移除重复项

                processedArray.sort((a, b) => {
                    const nameA = a.toUpperCase();                                  // 不区分大小写
                    const nameB = b.toUpperCase();

                    if (nameA < nameB) {
                        return -1;
                    }
                    if (nameA > nameB) {
                        return 1;
                    }
                    return 0;
                });

                this.highlightedText = this.originalText = processedArray.join(",　");
            })
            .catch(error => {
                ElMessage.error('Oops, Error fetching file content.');
                console.error('Oops, Error fetching file content.', error);
            });
    },
    computed: {
        trimmedSearchKeyword() {
            return this.searchKeyword.trim();
        },

        getColumnSpan() {
            return this.screenWidth < 768 ? 24 : 16;
        },
    },
    mounted() {
        this.screenWidth = window.innerWidth;

        this.player = document.getElementById('player');
        this.bindEvents();
        this.random();
    },
};
</script>

<style>
html {
    font-size: 16px; /* 设置默认字体大小 */
}

.header_title {
    font-size: 2em;
}

.blockquote {
    font-size: 0.8em;
}

@media screen and (max-width: 768px) {
    html {
        font-size: 14px; /* 在小屏幕下设置较小的字体大小 */
    }

    .el-main {
        --el-main-padding: 16px;
    }

    .el-card {
        --el-card-padding: 12px;
    }

    .el-input__inner {
        font-size: 0.8em;
    }
}

@media screen and (max-width: 480px) {
    html {
        font-size: 12px; /* 在更小的屏幕下设置更小的字体大小 */
    }

    .header_title {
        font-size: 1.6em;
    }

    .el-main {
        --el-main-padding: 16px;
    }

    .el-card {
        --el-card-padding: 12px;
    }

    .el-form-item__label {
        font-size: 1em;
    }
}

.box-card {
    width: 100%;
}

.yellow {
    background-color: yellow;
}

.content {
    float: left;
    width: 260px;
    height: 400px;
    background-color: white;
    margin-right: 8px;
}
</style>
