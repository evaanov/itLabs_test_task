<template>
    <div class="users" v-for="user in users">
      <div class="user">
        <p id="index">{{ user.id }}</p>
        <p id="name">{{ user.name }}</p>
        <p id="company">{{ user.company }}</p>
        <p id="group">{{ user.group }}</p>
        <div class="here" v-if="user.isHere"></div>
        <div class="not_here" v-else></div>
      </div>
    </div>
</template>

<script>
export default { 
    props: { 
        users: { 
            type: Array,
            required: true
        }
    }
}
</script>

<style>
     .here { 
    border-radius: 30px;
    width: 59px;
    height: 59px;
    background-color: #80BB00;
  }

  .not_here { 
    border-radius: 30px;
    width: 59px;
    height: 59px;
    background-color: #EC5937;
  }

  .user { 
    display: flex;
    flex-direction: row;
    width: 92%;
    max-width: 1892px;
    margin: auto;
    margin-top: 50px;
    font-size: 30px;
    line-height: 40.85px;
    justify-content: space-between;
  }

  #index {
    width: 68px;
    margin: 0;
    margin-right: 7%;
  }

  #name { 
    width: 394px;
    margin: 0;
    margin-right: 5%;
  }

  #company {
    width: 210px;
    margin: 0;
    margin-right: 9%;
  }

  #group {
    width: 153px;
    margin: 0;
    margin-right: 23%;
  }
</style>