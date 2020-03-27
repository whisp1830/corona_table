# CoronaVirus实时数据表

第一个前端demo vue+axios+sorttable

显示实时的新冠肺炎全球感染数据，可点击表头进行排序

1. vue渲染模板
2. axios异步请求API数据
3. sorttable对表格中元素排序

<!DOCTYPE html>

<html>

<head>

    <meta charset="utf-8"/>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

    <script src="https://cdn.bootcss.com/axios/0.19.2/axios.js"></script>

    <script src="https://www.kryogenix.org/code/browser/sorttable/sorttable.js"></script>

</head>



<body>

<div id="app">

​    <h1>Coronavirus Realtime Infection</h1>

  

​    <section v-if="errored">

      <p>Connect failed</p>

​    </section>

​    <section v-else>



                <table border="1" class="sortable">

​                    <tr>

​                        <th>国名</th>

​                        <th class="sorttable_numeric">确诊数</th>

​                        <th class="sorttable_numeric">今日确诊</th>

​                        <th class="sorttable_numeric">死亡数</th>

​                        <th class="sorttable_numeric">治愈数</th>

​                        <th class="sorttable_numeric">现存确诊</th>

​                        <th class="sorttable_numeric">每百万人确诊</th>

​                        <th class="sorttable_numeric">每百万人死亡</th>

​                    </tr>

​                    <template v-if="loading">加载中...</template>

​                    <template v-else>

​                    <tr

​                        v-for="country in info"

​                        class="item"

​                    \> 

​                        <td>{{ country.country.trim() }}</th>

​                        <td>{{ country.cases }}</td>

​                        <td>{{ country.todayCases }}</td>

​                        <td>{{ country.deaths }}</td>

​                        <td>{{ country.recovered }}</td>

​                        <td>{{ country.active }}</td>

​                        <td>{{ country.casesPerOneMillion }}</td>

​                        <td>{{ country.deathsPerOneMillion }}</td>

​                    </tr>  

​                    </template>               

​                </table>

​    </section>

</div>

</body>





<script>

​    new Vue({

​    el: '#app',

​    data () {

​        return {

​        info: null,

​        loading: true,

​        errored: false

​        }

​    },

​    filters: {

​        currencydecimal (value) {

​        return value.toFixed(2)

​        }

​    },

​    mounted () {

​        axios

​        .get('https://corona.lmao.ninja/countries?sort=country')

​        .then(response => {

​            this.info = response.data

​        })

​        .catch(error => {

​            console.log(error)

​            this.errored = true

​        })

​        .finally(() => this.loading = false)

​    }

​    })

</script>

</html>