<script setup lang="ts">
    import { onMounted, ref } from "vue"
    
    const githubInfo = ref<GithubRepo[]>([])
    const count = ref(0)

    interface GithubRepo {
        full_name: string
        description: string | null
        html_url: string
        owner: {
            avatar_url : string
        }
    }

    async function loadingApi() {
        try {
            const response = await fetch("https://api.github.com/users/jordan-lima/repos")
            const data = await response.json()
            githubInfo.value = data
        } catch (e) {
            console.error("Erro ao buscar informações do github: ", e)
        }
    }

    onMounted(() => {
        loadingApi()
    })

    const handleClickNext = () => {
        if (count.value === githubInfo.value.length - 1) {
            count.value = 0
        } else {
            count.value++
        }    
    }

    const handleClickPrevious = () => {
        if (count.value === 0) {
            count.value = githubInfo.value.length - 1
        } else {
            count.value--
        } 
    }

    const accessGitProject = (url_git : string) => {
        window.open(url_git, "_blank")
    }

    const automaticSlide = () => {
        setInterval(() => {
            handleClickNext()
        }, 2000)
    }

    automaticSlide()

</script>

<template>
  <div class="sm:flex justify-center items-center w-full sm:mb-0 mb-5">
      <div class="sm:flex sm:justify-center items-center gap-2 bg-amber-200 border-1 sm:h-[150px]" v-if="githubInfo.length > 0">
        <div class="flex justify-center sm:h-[150px] items-center px-[30px] bg-[#bbeaf0] border-y-1 border-r-1">
            <img :src="githubInfo[count].owner.avatar_url" class="w-[100px] sm:rounded-full sm:min-w-[130px] sm:h-[130px] my-2" alt="Avatar do Github">
        </div>
        <div class="sm:py-auto py-5">
            <div class="flex flex-col w-full sm:h-full px-5"> 
                <h3 class="flex justify-center items-center font-bold">
                    {{ githubInfo[count].full_name }}
                </h3>        
                <p class="flex justify-center items-center ">
                    {{ githubInfo[count].description }}
                </p>
    
            </div>
            <div class="flex justify-center items-center gap-5">
                <button @click="handleClickPrevious" class="bg-[#f06b6b] border-1 p-2 rounded-full font-asimovian">↜ Prev</button>
                <button @click="accessGitProject(githubInfo[count].html_url)" class="bg-[#6ba5f0] border-1 p-2 rounded-full font-asimovian">🤯 Enter</button>
                <button @click="handleClickNext" class="bg-[#86f06b] border-1 p-2 rounded-full font-asimovian">Next ↝</button>
        
            </div>
        </div>
    </div>
    </div>
</template>