<template>
  <div class="body">
    <div class="header">
      <div class="left">
        <img class="logo" src="../lib/logo2.png"/>
        <input class="search" type="text" v-model="searchQuery" placeholder="Поиск по имени">
        <button class="add_btn" @click="this.popupVisible = !this.popupVisible">Добавить</button>
      </div>
      <div class="right">
        <p class="visitors">Посетители</p>
        <div class="count">
          <p class="green">280</p >
          <p >/</p>
          <p class="red">35</p>
        </div>
      </div>
    </div>
    <div class="line">
      <p id="number">Номер</p>
      <p id="fio">ФИО</p>
      <p id="comp">Компания</p>
      <p id="gruppa">Группа</p>
      <p id="here">Присутствие</p>
    </div>
    <add-user v-model:show="popupVisible" :users="users" @create="createUser" />
    <users-list :users="searchedUsers"/>
    <div class="filter">
      <p>Фильтровать по:</p>
      <div class="filters">
        <p :class="{active: this.active.first}" @click="firstActive" >Отсутсвующим</p>
        <p :class="{active: this.active.second}" @click="secondActive">Присутствующим</p>
        <p :class="{active: this.active.default}" @click="defaultActive">Без фильра</p>
      </div>
    </div>
  </div>
</template>

<script>
  import UsersList from '@/components/UsersList.vue'
  import AddUser from './components/AddUser.vue';

  export default { 
    components: { 
      UsersList,
      AddUser
    },
    data () { 
      return { 
        users: [
          {id: 1, name: 'Зубенко Михаил Петрович', company: 'ООО "АСОЛЬ"', group: 'Прохожий', isHere: true},
          {id: 2, name: 'Зубенко Михаил Петрович', company: 'ООО "АСОЛЬ"', group: 'Партнер', isHere: false},
        ],
        popupVisible: false,
        searchQuery: '',
        filter: 'none',
        active: {
          first: false,
          second: false,
          default: true
        }
      }
    },
    methods: { 
      createUser(post) { 
        this.users.push(post)
      },
      firstActive() { 
        this.active.first = true;
        this.active.second = false;
        this.active.default = false;
        this.filter = 'not here'
      },
      secondActive() { 
        if (this.active.second) {
          this.active.first = false;
          this.active.second = false;
          this.active.default = true;
          this.filter = 'none'
        } else { 
          this.active.first = false;
          this.active.second = true;
          this.active.default = false;
          this.filter = 'here'
        }
        
      },
      defaultActive() { 
        this.active.first = false;
        this.active.second = false;
        this.active.default = true;
        this.filter = 'none'
      }
    },
    computed: { 
      searchedUsers() { 
        const searched = [...this.users].filter((user) => {
            return user.name.toLowerCase().includes(this.searchQuery.toLowerCase()) 
            || user.company.toLowerCase().includes(this.searchQuery.toLowerCase())
          });

        if (this.filter === "none") { 
          return searched;
        } else if (this.filter === 'not here') {
          return searched.filter((u) => { 
            return !u.isHere
          })
        } else if (this.filter === 'here') {
          return searched.filter((u) => { 
            return u.isHere
          })
        }
      }
    }
  }
</script>

<style scoped>
  * { 
    margin: 0;
    padding: 0;
    font-family: 'Open Sans', sans-serif;
  }

  .body { 
    display: flex;
    flex-direction: column;
    margin: 0;
    padding: 0;
  }

  .header { 
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    width: 92%;
    height: 113.4px;
    margin: 24px auto;
  } 

  .left { 
    display: flex;
    flex-direction: row;
    gap: 40px;
  }

  .logo { 
    width: 187.89px;
    height: 89.4px; 
  }

  .search { 
    width: 346px;
    height: 52px;
    padding: 0px 19px;
    border: none;
    border-radius: 7px;
    box-shadow: 0px 0px 20px 0px rgba(0, 0, 0, 0.09);
    align-items: baseline;
    
    font-size: 16px;
    line-height: 21.79px;
    margin-top: 37px;
  }

  .add_btn { 
    width: 273px;
    height: 52px;
    background-color: #4CAF50;
    color: white;
    text-align: center;
    border: none;
    border-radius: 7px;
    font-size: 24px;
    line-height: 28.13px;
    margin-top: 37px;
  }

  .right { 
    display: flex;
    flex-direction: column;
    gap: 5px;
    font-size: 30px;
    line-height: 40.85px;
    font-weight: 700;
    color: #4E3000;
  }

  .count { 
    display: flex;
    flex-direction: row;
    gap: 8px;
  }

  .green { 
    color: #80BB00;
  }

  .red { 
    color: #EC5937;
  }

  .line { 
    width: 92%;
    max-width: 1948px;
    display: flex;
    flex-direction: row;
    margin: auto;
    font-size: 20px;
    line-height: 27.24px;
    font-weight: 600;
    color: #4E3000;
    border-bottom: 4px solid #E9E9E9;
    justify-content: left;
  }

  #number {
    width: 68px;
    margin: 0;
    margin-right: 9%;
  }

  #fio { 
    width: 93px;
    margin: 0;
    margin-right: 25%;
  }

  #comp {
    width: 104px;
    margin: 0;
    margin-right: 16.3%;
  }

  #gruppa {
    width: 72px;
    margin: 0;
    margin-right: 23%;
  }

  #here {
    width: 119px;
    margin: 0;
    margin-right: 3%;
  }

  .filter { 
    display: flex;
    flex-direction: row;
    gap: 73px;
    width: 92%;
    margin: auto;
    margin-top: 50px;
  }
  
  .filter p { 
    font-size: 30px;
    line-height: 40.85px;
    font-weight: 700;
    color: #4E3000;
    margin: 0;
  }

  .filters { 
    display: flex;
    flex-direction: row;
    width: 674px;
    justify-content: space-between;
  }

  .filters p { 
    font-size: 25px;
    line-height: 34.05px;
    font-weight: 400;
    color: #4E3000;
    margin-top: 5px;
    cursor: pointer;
  }

  .filters .active { 
    padding: 10px 20px;
    color: white;
    background-color: #C4C4C4;
    border-radius: 20px;
    margin-top: 0;
  }
</style>
