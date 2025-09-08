<template>
    <nav class="flex justify-between items-center p-5 bg-amber-100">
        <div class="flex sm:w-[65px] w-[50px] h-8 justify-center items-center">
            <img src="@/assets/img/logo.png" alt="logo da empresa" class="">

        </div>
        <div class="flex justify-end gap-5 font-epunda-slab sm:text-[1.3em]">
            <RouterLink to="/">Home</RouterLink>
            <RouterLink to="/curriculum">Curriculo</RouterLink>
            <RouterLink to="/univesp">Univesp</RouterLink>
            <RouterLink to="/about">Sobre</RouterLink>

        </div>
    </nav>


</template>