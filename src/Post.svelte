<script>
  export let postData;
  console.log(postData.hide)
</script>

<style>
  .post {
    position: relative;
    background-color: #fff;
    box-shadow: 0 2px 4px rgba(0,0,0,0.3);
    border-radius: 5px;
    padding: 20px;
    margin: 40px 0;
    display: flex;
    width: 80vw;
    max-width: 800px;
  }

  .hide {
    display: none;
  }

  .number {
    position: absolute;
    box-shadow: 0 2px 4px rgba(0,0,0,0.3);
    top: -15px;
    left: -15px;
    font-size: 15px;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background: #fff;
    color: #40b3ff;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 7px 10px;
  }

  .post-title {
    margin: 0;
  }

  .post-body {
    margin: 15px 0 0;
    line-height: 1.3;
  }
</style>

<div class="post" class:hide={postData.hide}>
  {#if postData}
    <div class="number">
      {postData.id}
    </div>
  {/if}
  {#if postData}
    <div class="post-info">
      <h2 class="post-title">{postData.title}</h2>
      <p class="post-body">{postData.body}</p>
    </div>
  {/if}
</div>