<template>
    <Layout>
        <div
            class="container flex flex-col flex-wrap items-center justify-center mx-auto grid grid-cols-1 px-auto md:flex-row "
        >
            <div class="max-w-xl mx-0 mx-auto px-auto">
                <h1
                    class="mt-4 mb-6 text-2xl font-bold leading-tight text-center text-primary"
                >
                    Blog
                </h1>

                <ul>
                    <li v-for="{ node } in $page.posts.edges" :key="node.id">
                        <g-link :to="node.path">
                            <div
                                class="p-20 m-4 overflow-hidden border-2 border-solid shadow-lg border-primary max-auto-sm rounded-md"
                            >
                                <g-image
                                    alt="Example image"
                                    :src="node.image.file.url"
                                    blur="70"
                                    width="135"
                                    height="30"
                                />
                                <h1 class="text-2xl font-bold text-primary">
                                    {{ node.title }}
                                </h1>
                                <p class="pt-5 text-darkgray">
                                    {{ node.description }}
                                </p>
                                <p
                                    class="pt-5 text-sm font-normal text-primary"
                                >
                                    Posted on {{ node.date }}
                                </p>
                            </div>
                        </g-link>
                    </li>
                </ul>
            </div>
        </div>
        <div class="pages">
            <Pager
                v-if="$page.posts.pageInfo.totalPages > 1"
                :info="$page.posts.pageInfo"
            />
        </div>
    </Layout>
</template>

<page-query>
   
     query Posts($page: Int) { 
     posts: allContentfulPortfolioBlog(sortBy: "date", order:
  DESC, perPage: 3, page: $page)
    @paginate { totalCount pageInfo { totalPages
  currentPage } 
    edges { node { id, path, image { file { url } }, title, body, date (format:
  "MMMM D, Y") } } } }

    </page-query>

<script>
import { Pager } from "gridsome";

export default {
    components: {
        Pager,
    },
    metaInfo: {
        title: "Blog",
    },
};
</script>

<style>

.pages a {
    padding: 1rem;
 }

 .pages {
     margin: 2rem auto;
     text-align: center;
     font-size: 2rem;
 }

 .pages a:hover {
     color: orange;
 }


 


 

</style>
