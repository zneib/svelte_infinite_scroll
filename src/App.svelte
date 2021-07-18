<script>
  import Post from './Post.svelte'
  import Loader from './Loader.svelte'
	import { onMount } from 'svelte'
  let posts = []
  let page = 1
  let limit = 5
  let loading = false

  async function getData() {
    const res = await fetch(`https://jsonplaceholder.typicode.com/posts?_limit=${limit}&_page=${page}`)
    const data = await res.json()
    const extra = await data.map(item => { 
      return { ...item, hide: false }
    })
    posts = [...posts, ...extra]
  }

  function showLoader() {
    loading = true
    setTimeout(() => {
      loading = false

      setTimeout(() => {
        page += 1
        getData()
      }, 300);
    }, 1000);
  }

  function filterData(e) {
    const term = e.target.value.toUpperCase()
    const filteredPosts = posts.map(post => {
      const title = post.title.toUpperCase()
      const body = post.body.toUpperCase()

      if (title.indexOf(term) > -1 || body.indexOf(term) > -1) {
        post.hide = false
      } else {
        post.hide = true
      }
      return post
    })
    posts = [...filteredPosts]
  }

	onMount(async () => {
		const res = await fetch(`https://jsonplaceholder.typicode.com/posts?_limit=${limit}&_page=${page}`)
    const data = await res.json()
    const extra = await data.map(item => { 
      return { ...item, hide: false }
    })
    posts = extra

    window.addEventListener('scroll', () => {
      const { scrollTop, scrollHeight, clientHeight } = document.documentElement

      if (scrollTop + clientHeight >= scrollHeight - 5) {
        showLoader()
      }
    })
	});
</script>

<style>
	h1 {
		color: #ff3e00;
		font-size: 3em;
		font-weight: 300;
    font-variant-caps: small-caps;
	}

  .filter {
    outline: '#40b3ff';
  }
</style>

<h1>Svelte Infinite Scroll</h1>
<div class="filter-container">
  <input type="text" id="filter" class="filter" placeholder="Filter Posts..." on:input={filterData}>
</div>
<div id="post-container">
  {#each posts as post}
    <Post postData={post} />
  {/each}
</div>
<Loader loading={loading} />