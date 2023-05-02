<template>
    <div class="result">
        <div class="title">{{ results[ResultsIndex].title }}</div>
        <div class="desc">
            {{ results[ResultsIndex].desc }}
        </div>
    </div>
</template>

<script>
export default {
    props: [
        'results',
        'totalCorrect'
    ],
    computed: {
        ResultsIndex() {
            let index = 0

            this.results.forEach((item, i) => {
                if(item.min <= this.totalCorrect && item.max >= this.totalCorrect) 
                    index = i 
            })

            return index
        }
    }
}
</script>