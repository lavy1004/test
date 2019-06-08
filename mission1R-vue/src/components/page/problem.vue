<template>
        <section class="main">
			<section class="screen">
				<div class="problem">
                    <div class="problem-stub" v-for="(item, index) in list.problems" :key="index">
                        <span class="id">{{item.id}}</span>.
                        <span class="problem-text">{{item.problem_text}}</span>

                        <div class="answer-user">
                            <div class="answer-stub-choice" v-for="(item2,index2) in choices" :key="index2">
                                <span class="label"></span>
                                <span v-for="(item3,index3) in item2[index]" :key="index3">
                                    <input type="radio" value="1" name="choice_17217">
                                    <span class="choice">{{item3}}</span>
                                </span>
                            </div>
                        </div>
                        <div class="answer-right"></div>
                    </div>
				</div>

				<aside class="main-result">
				</aside>
			</section>

			<footer class="main-footer">
				<button class="submit">제출</button>
			</footer>
		</section>

		<!-- <section class="templates">
			<div class="tmpl-problem-stub">
				<span class="id"></span>.
				<span class="problem-text"></span>

				<div class="answer-user"></div>
				<div class="answer-right"></div>
			</div>

			<div class="tmpl-answer-stub-choice">
				<span class="label"></span>

				<input type="radio" value="1" />
				<span class="choice"></span>

				<input type="radio" value="2" />
				<span class="choice"></span>

				<input type="radio" value="3" />
				<span class="choice"></span>

				<input type="radio" value="4" />
				<span class="choice"></span>

				<input type="radio" value="5" />
				<span class="choice"></span>
			</div>

			<div class="tmpl-answer-stub-text">
				<span class="label"></span>
				
				<input type="text" class="value" />
			</div>

			<div class="tmpl-answer-stub-draw">
				<span class="label"></span>
				
				<canvas class="canvas"></canvas>
			</div>

			<div class="tmpl-result-stub">
				<span class="id"></span>.
				<span class="result"></span>
			</div> -->
		<!-- </section> -->
</template>

<script>
import axios from 'axios'

export default {
    created () {
        axios({
        // config: { headers: {'Content-Type': 'multipart/form-data' }},
        method: 'get',
        url: '/api/fetchProblem',
        responseType: 'json',
        })
        .then((res) => {
            this.list = res.data
            let listflt = this.list.problems.filter((x)=> x.choices )
            
            let list2 = listflt.map((y)=> _.trim(y.choices,'[]'))
            
            let list3 = list2.map((z)=> z.split(','))
            console.log(list3)
            return this.choices.push(list3)
            
        })
        console.log(this.choices)
    },
    data () {
        return {
            list: [],
            choices: []
        }
    },
    computed: {
    }
}
</script>

<style>

</style>
