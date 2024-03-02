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
                                    提交新名单，更新：2024-01-27
                                </span>
                            </blockquote>

                            <div class="content">
                                <section id="main">
                                    <video id="player" src="https://dwz.mk/MVZVjy"
                                           autoplay controls="controls" width="100%" height="400px">
                                    </video>
                                </section>
                            </div>
                            <div v-html="highlightedText" style="font-size: 1em;"></div>
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
}
</style>
