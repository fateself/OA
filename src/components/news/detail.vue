<template>
    <div class="tmpl">
        <nav-bar title="新闻详情"></nav-bar>
        <div class="news-title">
            <p>{{news.title}}</p>
            <div>
                <span>{{news.click}}次点击</span>
                <span>分类:民生经济</span>
                <span>添加时间:{{news.add_time | format_date}}</span>
            </div>
        </div>
        <div class="news-content" v-html="news.content"></div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            //news
            news: {},
        }
    }, created() {
        //创建组件的时候获取参数，发起请求，挂载值到页面
        let id = this.$route.query.id;
        //发起请求http://webhm.top:8899/api/
        this.axios.get('getnew/' + id)
            .then(res => {
                this.news = res.data.message[0];
            })
            .catch(err => {
                console.log('获取新闻详情数据失败');
            });
    }
}
</script>
<style scoped>
.news-title p {
    color: #0a87f8;
    font-size: 20px;
    font-weight: bold;
}

.news-title span {
    margin-right: 30px;
}

.news-title {
    margin-top: 5px;
    border-bottom: 1px solid rgba(0, 0, 0, 0.2);
}


/*主体文章的左右距离*/

.news-content {
    padding: 10 5;
}
</style>
